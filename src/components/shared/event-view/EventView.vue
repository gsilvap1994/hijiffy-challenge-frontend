<template>
	<div class="event-view" :class="active ? 'active' : 'canceled'">
		<div class="title">
			{{ title }}
		</div>
		<div class="time">
			{{ formatTime(startDate) }} -
			{{ formatTime(endDate, true) }}
		</div>
	</div>
</template>

<script>
export default {
	name: 'EventView',
	props: {
		title: {
			required: false,
			type: String,
		},
		startDate: {
			required: false,
			type: Date,
		},
		endDate: {
			required: false,
			type: Date,
		},
		active: {
			required: true,
			type: Boolean,
		},
	},
	methods: {
		formatTime(date, ampm) {
			let hours = new Date(date).getHours();
			let minutes = new Date(date).getMinutes();
			const amOrPm = hours > 12 ? 'pm' : 'am';
			hours = hours % 12;
			hours = hours ? hours : 12;
			minutes = minutes < 10 ? `:0${minutes}` : `:${minutes}`;
			minutes = minutes === ':00' ? '' : minutes;

			return `${hours}${minutes}${ampm ? amOrPm : ''}`;
		},
	},
};
</script>

<style lang="scss" scoped>
.event-view {
	border-radius: $default-border-radius;
	padding: 0.5rem;
	font-weight: 900;
	font-size: small;
	margin-bottom: 0.5rem;

	&.active {
		background-color: $light-primary-blue;
		color: #fff;
	}

	&.canceled {
		background-color: #fff;
		color: $light-primary-blue;
		border: 1px solid $light-primary-blue;
		text-decoration: line-through;
	}
}
</style>
