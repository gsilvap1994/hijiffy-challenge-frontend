<template>
	<app-shared-modal
		:lightTheme="lightTheme"
		v-show="isModalVisible"
		@modalClose="modalClose"
	>
		<template v-slot:header>
			<div class="date-view" :class="lightTheme ? '' : 'dark'">
				<header>
					<strong>CALENDAR</strong>
				</header>
				<div class="date">
					<strong>
						{{ formatDate(new Date()) }}
					</strong>
				</div>
			</div>
			<div class="close" :class="lightTheme ? '' : 'dark'" @click="modalClose">
				X
			</div>
		</template>

		<template v-slot:body>
			<div
				class="days"
				:class="lightTheme ? '' : 'dark'"
				v-for="(day, index) of schedule"
				:key="`schedule-day-${day.id}`"
			>
				<div class="first" v-if="!index">
					<div class="header">Today</div>
					<app-shared-event-view
						v-for="event of day.events"
						:key="`schedule-day-${day.id}-event-${event.id}`"
						:title="event.title"
						:startDate="event.startDate"
						:endDate="event.endDate"
						:active="event.active"
						:lightTheme="lightTheme"
					/>
				</div>
				<div class="other" v-if="index">
					<div class="header">{{ formatDate(day.date) }}</div>
					<app-shared-event-view
						v-for="event of day.events"
						:key="`schedule-day-${day.id}-event-${event.id}`"
						:title="event.title"
						:startDate="event.startDate"
						:endDate="event.endDate"
						:active="event.active"
						:lightTheme="lightTheme"
					/>
				</div>
			</div>
		</template>
	</app-shared-modal>
</template>

<script>
import Modal from '../shared/modal/Modal.vue';
import EventView from '../shared/event-view/EventView.vue';
export default {
	name: 'CalendarView',
	components: {
		'app-shared-modal': Modal,
		'app-shared-event-view': EventView,
	},
	data() {
		return {
			schedule: [
				{
					id: 0,
					date: new Date(),
					events: [
						{
							id: 0,
							active: true,
							title: 'Daily stand up',
							startDate: new Date(new Date().setHours(9, 30)),
							endDate: new Date(new Date().setHours(10, 0)),
						},
						{
							id: 1,
							active: true,
							title: 'Google Apps',
							startDate: new Date(new Date().setHours(10, 15)),
							endDate: new Date(new Date().setHours(11, 0)),
						},
						{
							id: 2,
							active: true,
							title: 'Server Events async',
							startDate: new Date(new Date().setHours(11, 30)),
							endDate: new Date(new Date().setHours(12, 0)),
						},
						{
							id: 3,
							active: true,
							title: 'HR',
							startDate: new Date(new Date().setHours(11, 30)),
							endDate: new Date(new Date().setHours(12, 0)),
						},
					],
				},
				{
					id: 1,
					date: new Date().setDate(new Date().getDate() + 1),
					events: [
						{
							id: 0,
							active: false,
							title: 'Daily stand up',
							startDate: new Date(new Date().setHours(9, 30)),
							endDate: new Date(new Date().setHours(10, 0)),
						},
					],
				},
			],
		};
	},
	props: {
		isModalVisible: {
			required: true,
			type: Boolean,
		},
		lightTheme: {
			required: true,
			type: Boolean,
		},
	},
	methods: {
		formatDate(date) {
			const weekday = new Date(date).toLocaleString('default', {
				weekday: 'short',
			});
			const month = new Date(date).toLocaleString('default', {
				month: 'short',
			});
			const day = new Date(date).getDate();
			return `${weekday}, ${month} ${day}`;
		},
		modalClose() {
			this.$emit('modalClose');
		},
	},
};
</script>

<style lang="scss" scoped>
.date-view {
	header {
		color: $light-color-text;
		font-size: $font-small;
	}

	&.dark {
		color: $dark-light-blue;
		header {
			color: $dark-color-text;
		}
	}
}
.close {
	color: $light-color-text;
	&.dark {
		color: $dark-color-text;
	}
	cursor: pointer;
	font-size: $font-large;
}

.days {
	&.dark {
		.header {
			border-bottom: 1px solid $dark-primary-soft-black;
		}
		.first {
			.header {
				color: $dark-light-blue;
			}
		}
		.other {
			color: $dark-color-text;
		}
	}
	.header {
		padding: 0 0.75rem 1rem;
		margin: 0 -0.75rem 1rem;
		font-weight: 900;
		border-bottom: 1px solid #dadce0;
	}
	.first {
		.header {
			color: $light-primary-blue;
		}
	}
	.other {
		margin-top: 2rem;
	}
}
</style>
