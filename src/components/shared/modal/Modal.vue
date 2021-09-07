<template>
	<div class="modal-backdrop" @click="close">
		<div class="modal" @click="handleModalClick($event)">
			<header class="modal-header">
				<slot name="header"> This is the default title! </slot>
			</header>

			<section class="modal-body">
				<slot name="body"> This is the default body! </slot>
			</section>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Modal',
	methods: {
		close() {
			this.$emit('modalClose');
		},
		handleModalClick($event) {
			$event.stopPropagation();
		},
	},
};
</script>

<style lang="scss" scoped>
.modal-backdrop {
	position: fixed;
	top: 0;
	bottom: 0;
	left: 0;
	right: 0;
	background-color: rgba(10, 87, 134, 0.5);
	display: flex;
	justify-content: center;
	align-items: center;
	z-index: 99999999999999;
	cursor: pointer;

	.modal {
		background: #ffffff;
		overflow-x: auto;
		display: flex;
		flex-direction: column;
		width: 25vw;
		min-width: 200px;
		max-width: 350px;
		cursor: default;
		border-radius: $default-border-radius;
		.modal-header {
			padding: 1.5rem;
			display: flex;
			position: relative;
			border-bottom: 1px solid #f1f3f4;
			color: $light-primary-blue;
			justify-content: space-between;
		}
		.modal-body {
			position: relative;
			padding: 1.5rem 0.75rem;
			max-height: 70vh;
			overflow: auto;
		}
	}
}
</style>
