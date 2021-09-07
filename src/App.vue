<template>
	<app-header
		:isAuthenticated="true"
		:hasNotifications="true"
		:imgSrc="require(`@/assets/images/icons/profile.jpg`)"
	/>
	<main class="main-page">
		<div class="table-actions">
			<div class="filter">
				<span>Company: </span>
				<select v-model="filterCompany" class="select" name="select">
					<option value="" selected>All</option>
					<option
						v-for="(company, index) of companies"
						:key="`companies-select-option${index}`"
						:value="company"
					>
						{{ company }}
					</option>
				</select>
			</div>
			<app-shared-button :type="'button'" :label="'Add Contact'" />
		</div>
		<app-contact-list
			:contacts="filterCompanies"
			@showContactModal="showContactModal($event)"
		/>
	</main>
	<app-shared-pager
		:currentPage="currentPage"
		:totalPages="totalPages"
		:perPage="perPage"
		:perPageModel="perPageModel"
		@previousPage="previousPage"
		@nextPage="nextPage"
		@perPageChange="perPageChange($event)"
	/>
	<app-footer />
	<app-calendar-view
		:isModalVisible="isModalVisible"
		@modalClose="closeContactModal"
	/>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import axios from 'axios';

import Header from './components/header/Header.vue';
import Footer from './components/footer/Footer.vue';
import ContactList from './components/contact-list/ContactList.vue';
import CalendarView from './components/calendar-view/CalendarView.vue';
import Button from './components/shared/button/Button.vue';
import Pagination from './components/shared/pagination/Pagination.vue';

export default defineComponent({
	name: 'App',
	components: {
		'app-header': Header,
		'app-footer': Footer,
		'app-contact-list': ContactList,
		'app-calendar-view': CalendarView,
		'app-shared-button': Button,
		'app-shared-pager': Pagination,
	},
	computed: {
		filterCompanies() {
			if (this.filterCompany) {
				return this.contacts.filter(
					(contact) =>
						contact.company_name.toLowerCase() ===
						this.filterCompany.toLowerCase(),
				);
			}
			return this.contacts;
		},
	},
	data() {
		return {
			contacts: [],
			companies: [],
			isModalVisible: false,
			filterCompany: '',
			currentPage: 0,
			totalPages: 1,
			perPage: 10,
			perPageModel: [],
		};
	},
	async created() {
		try {
			this.initState();
		} catch (e) {
			console.log(e);
		}
	},
	methods: {
		showContactModal(id) {
			console.log(id);
			this.isModalVisible = true;
		},
		closeContactModal() {
			this.isModalVisible = false;
		},
		previousPage() {
			this.currentPage -= 1;
			this.initState();
		},
		nextPage() {
			this.currentPage += 1;
			this.initState();
		},
		perPageChange($event) {
			this.perPage = +$event;
			this.currentPage = 0;
			this.initState();
		},

		async initState() {
			const res = await axios.get(
				`http://localhost:3000/contacts?limit${this.perPage}&offset=${this.currentPage}`,
			);
			this.contacts = res.data;
			const totalRecords = this.contacts.length;
			this.perPage = this.perPage ? this.perPage : totalRecords;
			if (totalRecords !== this.perPage) {
				console.log(this.currentPage * this.perPage);
				console.log(this.perPage);
				console.log(this.contacts.slice(2, this.perPage));
				this.contacts = this.contacts.slice(
					this.currentPage * this.perPage,
					this.currentPage * this.perPage + this.perPage,
				);
			}
			this.perPageModel = Array.from({ length: totalRecords }, (_, i) => i + 1);
			this.totalPages = totalRecords / this.perPage;
			this.companies = this.contacts.map((contact) => contact.company_name);
			this.companies = this.companies.sort();
		},
	},
});
</script>

<style lang="scss">
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
}

body {
	margin: 0;
	color: $light-color-text;
}

.main-page {
	background-color: $light-primary-light-grey;
	padding-top: calc(100px + 2rem);

	.contact-list,
	.table-actions {
		width: 90%;
		margin: 0 auto;
		padding-bottom: 2rem;
	}

	.table-actions {
		display: flex;
		align-items: baseline;
		justify-content: space-between;
	}
}

.select {
	border: none;
	background: transparent;
	color: $light-primary-blue;
}
</style>
