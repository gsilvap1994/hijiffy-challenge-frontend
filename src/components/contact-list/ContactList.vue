<template>
	<div class="contact-list" :class="lightTheme ? '' : 'dark'">
		<table>
			<thead :class="contacts.length > 4 ? 'reduced-size' : 'full-size'">
				<tr>
					<th>
						<input
							type="checkbox"
							name="check-all"
							id="check-all-contact-list"
						/>
					</th>
					<th>Name</th>
					<th>Email</th>
					<th>Company name</th>
					<th>Role</th>
					<th>Recent activity</th>
				</tr>
			</thead>
			<tbody>
				<tr
					@click="showContactModal(contact.id)"
					v-for="contact of contacts"
					:key="`contacts-tr-${contact.id}`"
				>
					<td>
						<input
							type="checkbox"
							:name="`check-contact-${contact.id}`"
							:id="`check-contact-${contact.id}`"
						/>
					</td>
					<td>
						<div class="name">
							<div
								:style="{
									backgroundColor: getRandomColor(),
									color: '#FFF',
								}"
								class="first-letter"
							>
								{{ contact.name.charAt(0) }}
							</div>
							<span>{{ contact.name }}</span>
						</div>
					</td>
					<td>{{ contact.email }}</td>
					<td>{{ contact.company_name }}</td>
					<td>{{ contact.role }}</td>
					<td>{{ formatDate(contact.recent_activity) }}</td>
				</tr>
			</tbody>
		</table>
	</div>
</template>

<script>
export default {
	name: 'ContactList',

	data() {
		return {
			backgroundColor: {
				red: '',
				green: '',
				blue: '',
			},
		};
	},
	methods: {
		formatDate(date) {
			const month = new Date(date).toLocaleString('default', {
				month: 'short',
			});
			const day = new Date(date).getDate();
			const year = new Date(date).getFullYear();
			return `${month} ${day}, ${year}`;
		},
		getRandomColor() {
			const red = Math.floor(Math.random() * 255) + 1;
			const green = Math.floor(Math.random() * 255) + 1;
			const blue = Math.floor(Math.random() * 255) + 1;
			this.backgroundColor.red = red;
			this.backgroundColor.green = green;
			this.backgroundColor.blue = blue;

			return `rgb(${red}, ${green}, ${blue})`;
		},
		showContactModal($event) {
			this.$emit('showContactModal', $event);
		},
	},
	props: {
		contacts: {
			required: true,
			type: Array,
		},
		lightTheme: {
			required: true,
			type: Boolean,
		},
	},
};
</script>

<style lang="scss" scoped>
.contact-list {
	table {
		width: 100%;
		border-collapse: collapse;
		border-radius: $default-border-radius;
		thead {
			background-color: #fff;
			border-bottom: 1px solid $light-primary-light-grey;
			border-top-left-radius: $default-border-radius;
			border-top-right-radius: $default-border-radius;
			display: table;
			table-layout: fixed;

			th {
				background-color: white;
				position: sticky;
				top: 0;
				padding: 1rem;
				border-top-left-radius: $default-border-radius;
				border-top-right-radius: $default-border-radius;
			}
		}

		tbody {
			background-color: #fff;
			color: #000;
			display: block;
			max-height: 280px;
			overflow-y: auto;
			border-bottom-left-radius: $default-border-radius;
			border-bottom-right-radius: $default-border-radius;

			tr {
				border-bottom-left-radius: $default-border-radius;
				border-bottom-right-radius: $default-border-radius;
				cursor: pointer;
				display: table;
				width: 100%;
				table-layout: fixed;
				&.checked {
					background-color: $light-primary-light-grey;
				}
			}
			td {
				padding: 1rem;
				text-align: center;
				border-bottom: 1px solid $light-primary-light-grey;

				.name {
					display: flex;
					align-items: center;
					.first-letter {
						border-radius: 1000px;
						width: 30px;
						height: 30px;
						display: flex;
						justify-content: center;
						align-items: center;
						margin-right: 10px;
						font-weight: bold;
					}
				}
			}
		}
	}
	&.dark {
		table {
			thead,
			thead th,
			tbody,
			tbody td {
				background-color: $light-color-text;
				border-color: $dark-primary-black;
				color: black;
			}
		}
	}
}

.full-size {
	width: 100%;
}

.reduced-size {
	width: calc(100% - 1em);
}
</style>
