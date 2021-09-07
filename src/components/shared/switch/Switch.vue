<template>
	<label class="switch">
		<input type="checkbox" @change="changeTheme" :checked="!light" />
		<span class="slider round"> </span>
		<img
			class="light"
			width="16"
			:src="require(`@/assets/images/icons/sun.png`)"
			alt="Light Theme"
		/>
		<img
			class="dark"
			width="16"
			:src="require(`@/assets/images/icons/moon.png`)"
			alt="Dark Theme"
		/>
	</label>
</template>

<script>
export default {
	name: 'Switch',
	props: {
		light: {
			required: true,
			type: Boolean,
		},
	},
	methods: {
		changeTheme() {
			this.$emit('changeTheme', !this.light);
		},
	},
};
</script>

<style lang="scss" scoped>
.switch {
	position: relative;
	display: inline-block;
	width: 60px;
	height: 34px;

	.light {
		position: absolute;
		left: 8px;
		top: 8px;
	}
	.dark {
		position: absolute;
		right: 8px;
		top: 8px;
	}

	input {
		opacity: 0;
		width: 0;
		height: 0;
	}

	input:checked + .slider {
		background-color: #fff;
	}

	input:focus + .slider {
		box-shadow: 0 0 1px #fff;
	}

	input:checked + .slider:before {
		-webkit-transform: translateX(26px);
		-ms-transform: translateX(26px);
		transform: translateX(26px);
		background-color: $light-primary-blue;
	}

	.slider {
		position: absolute;
		cursor: pointer;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background-color: $light-primary-blue;
		-webkit-transition: 0.4s;
		transition: 0.4s;

		&.round {
			border-radius: 34px;
			&:before {
				border-radius: 50%;
			}
		}

		&::before {
			position: absolute;
			content: '';
			height: 26px;
			width: 26px;
			left: 4px;
			bottom: 4px;
			background-color: white;
			-webkit-transition: 0.4s;
			transition: 0.4s;
		}
	}
}
</style>
