<template>
	<div class="pagination" :class="lightTheme ? '' : 'dark'">
		<div
			class="prev"
			@click="previousPage"
			:class="currentPage ? '' : 'disabled'"
		>
			<img
				class="icon"
				:src="require(`@/assets/images/icons/left-chevron.png`)"
				alt="Previous page icon"
			/>
			<span>Prev</span>
		</div>
		<div class="current">
			{{ currentPage + 1 }}
		</div>
		<div
			class="next"
			:class="currentPage + 1 === totalPages ? 'disabled  ' : ''"
			@click="nextPage"
		>
			<span>Next</span>
			<img
				class="icon"
				:src="require(`@/assets/images/icons/right-chevron.png`)"
				alt="Next page icon"
			/>
		</div>

		<div class="per-page">
			<span>Show:</span>
			<select class="select" @change="perPageChange($event)" name="">
				<option
					v-for="page of perPageModel"
					:key="`pagination-per-page-${page}`"
					:value="page"
					:selected="page === perPage"
				>
					{{ page }} per page
				</option>
			</select>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Pagination',
	props: {
		currentPage: {
			required: true,
			type: Number,
		},
		totalPages: {
			required: true,
			type: Number,
		},
		perPage: {
			required: true,
			type: Number,
		},
		perPageModel: {
			required: true,
			type: Array,
		},
		lightTheme: {
			required: true,
			type: Boolean,
		},
	},
	methods: {
		previousPage() {
			if (this.currentPage) {
				this.$emit('previousPage');
			}
		},
		nextPage() {
			if (this.currentPage + 1 !== this.totalPages) {
				this.$emit('nextPage');
			}
		},
		perPageChange($event) {
			this.$emit('perPageChange', $event.target.value);
		},
	},
};
</script>

<style lang="scss" scoped>
.pagination {
	background-color: $light-primary-light-grey;
	&.dark {
		background-color: $dark-primary-black;
	}
	display: flex;
	justify-content: center;
	align-items: baseline;
	font-size: 0.8rem;
	padding-bottom: 2rem;
	.current {
		font-weight: 900;
	}
	.prev,
	.next {
		cursor: pointer;
		margin: 0 0.5rem;

		&.disabled {
			cursor: default;
			color: #d4d6db;
		}
		.icon {
			width: 20px;
			margin-bottom: -6px;
		}
		span {
			margin: 0 0.5rem;
		}
	}
}
</style>
