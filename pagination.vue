<template>
	<div class="pagination-wrapper">
		<span class="list-total-items">{{ pagedata.total }} items</span>
		<nav class="pagination is-centered is-small">
			<a class="pagination-previous" 
				v-on:click.prevent="getPageClick(pagedata.current_page - 1)"
				v-show="pagedata.current_page > 1">
				<i class="fa fa-angle-double-left" aria-hidden="true"></i>
			</a>

			<a class="pagination-next" 
				v-on:click.prevent="getPageClick(pagedata.current_page + 1)"
				v-show="pagedata.current_page < pagedata.last_page">
				<i class="fa fa-angle-double-right" aria-hidden="true"></i>
			</a>
			
			<ul class="pagination-list">				
				<li v-for="page in pagedata.last_page">
					<a class="pagination-link" 
						v-bind:class="{'is-current': (pagedata.current_page == page)}"
						v-on:click.prevent="getPageClick(page)">
						{{ page }}
					</a>
				</li>
			</ul>
		</nav>
	</div>
</template>

<script>
    export default {
    	props: {
    		pagedata: {
    			type: Object,
    			required: true,
    			default: () => ({
    				current_page: 0,
					last_page: 0,
					total: 0
    			})
    		}
    	},
    	methods: {
    		getPageClick(page){
    			this.$emit('page-clicked', page);
    		}
    	}
    }
</script>