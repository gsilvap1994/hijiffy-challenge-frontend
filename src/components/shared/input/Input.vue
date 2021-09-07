<template>
	<div class="custom-input" :class="lightTheme ? '' : 'dark'">
		<img
			class="custom-input__image"
			:src="require(`@/assets/images/icons/search.svg`)"
			aria-hidden="true"
		/>
		<input
			:id="id"
			:type="type"
			:placeholder="placeholder"
			@input="onInputChange($event)"
		/>
	</div>
</template>

<script>
export default {
	props: {
		id: {
			required: true,
			type: String,
		},
		type: {
			required: true,
			type: String,
		},
		placeholder: {
			required: false,
			type: String,
		},
		lightTheme: {
			required: true,
			type: Boolean,
		},
	},

	methods: {
		onInputChange($event) {
			const { value } = $event.target;
			this.$emit('onInputChange', value);
		},
	},
};
</script>

<style lang="scss" scoped>
.custom-input {
	position: relative;
	&.dark {
		input {
			background-color: $dark-primary-soft-black;
		}
	}

	&__image {
		height: 14px;
		position: absolute;
		top: 5px;
		left: 2px;
	}
	input {
		border: none !important;
		padding: 0.25rem;
		padding-left: 20px;
		font-size: $font-small;
		outline: none;

		&::-webkit-input-placeholder {
			color: $light-color-text;
		}

		&:-ms-input-placeholder {
			color: $light-color-text;
		}

		&::placeholder {
			color: $light-color-text;
		}
	}
}
</style>
