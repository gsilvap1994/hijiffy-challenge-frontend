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

export default defineComponent({
	name: 'App',
	components: {
		'app-header': Header,
		'app-footer': Footer,
		'app-contact-list': ContactList,
		'app-calendar-view': CalendarView,
		'app-shared-button': Button,
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
		};
	},
	async created() {
		try {
			const res = await axios.get(`http://localhost:3000/contacts`);
			this.contacts = res.data;
			this.companies = this.contacts.map((contact) => contact.company_name);
			this.companies = this.companies.sort();
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
