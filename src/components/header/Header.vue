<template>
	<nav class="header">
		<div class="header__container">
		<div class="header__container__left">
			<div class="header__container__left__logo">
				Hijiffy
			</div>
			<div class="header__container__left__search">
				<app-shared-input 
					:id="'glb-search'"
					:placeholder="'Global search'"
					:type="'search'"
				/>
			</div>
		</div>
		<div class="header__container__profile" v-show="isAuthenticated">
			<div
				:class="hasNotifications ? 'notify' : ''"
				class="header__container__profile__notifications" >
				<img
					:src="require('@/assets/images/icons/bell.png')"
					alt="Notifications"
				/>
			</div>
			<div class="header__container__profile__image">
				<img :src="imgSrc" alt="Profile Image" />
			</div>
		</div>
		</div>
	</nav>
</template>

<script>
import Input from '../shared/input/Input.vue';

export default {

	name: 'Header',
	components: {
		'app-shared-input': Input,
	},

	props: {
		// depends on isAuthenticated
		hasNotifications: {
			required: false,
			type: Boolean,
		},
		isAuthenticated: {
			required: true,
			type: Boolean,
		},
		imgSrc: {
			required: false,
			type: String,
		},
	},
};
</script>

<style lang="scss" scoped>
	.header {
		position: fixed;
		top: 0;
		width: 100%;
		background-color: #fff;
		background-color: #fff;
		z-index: 1000000000;
		&__container {
			padding: 1.5rem 2.5rem;
			display: flex;
			justify-content: space-between;
			border: 1px solid $light-primary-light-grey;
			align-items: center;
			&__left {
				display: flex;
				align-items: center;
				&__logo {
					margin-right: 4rem;
					color: $light-primary-blue;
					font-weight: 800;
					font-size: $font-large;
				}
			}
			&__profile {
				display: flex;
				justify-content: center;
				align-items: center;
				&__image img {
					cursor: pointer;
					width: 42px;
					height: 42px;
					border-radius: 1000px;
				}
				&__notifications {
					margin-right: 3rem;
					cursor: pointer;
					position: relative;
					&.notify {
						&::after {
							content: '•';
							position: absolute;
							right: 1px;
							font-size: 42px;
							color: red;
							top: -17px;
						}
					}
					img {
						width: 28px;
						height: 28px;
						border-radius: 1000px;
						opacity: 0.4;
					}
				}
			}
		}
	}
</style>
