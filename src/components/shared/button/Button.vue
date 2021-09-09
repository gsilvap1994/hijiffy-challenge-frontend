<template>
	<button @click="btnClick()" class="button" :class="btnStyle" :type="type">
		{{ label }}
	</button>
</template>
<script>
export default {
	computed: {
		btnStyle() {
			if (!this.lightTheme) {
				return 'button-default dark';
			}
			if (this.buttonStyle === 'default' || !this.buttonStyle) {
				return 'button-default';
			}
			return 'button-danger';
		},
	},

	props: {
		type: {
			required: true,
			type: String,
		},
		label: {
			required: true,
			type: String,
		},
		buttonStyle: {
			type: String,
		},
		lightTheme: {
			required: true,
			type: Boolean,
		},
	},

	methods: {
		btnClick() {
			this.$emit('btnClick');
		},
	},
};
</script>

<style scoped lang="scss">
.button {
	display: inline-block;
	padding: 1rem 2rem;
	border-radius: $default-border-radius;
	font-weight: 800;
	cursor: pointer;
	border-color: $light-primary-blue;
	border-style: none;
}

.button-danger {
	background: firebrick;
	color: white;
}

.button-default {
	background: $light-primary-blue;
	color: white;

	&.dark {
		background-color: $dark-color-text;
		color: $dark-primary-black;
		border-color: $dark-primary-black;
	}
}
</style>
