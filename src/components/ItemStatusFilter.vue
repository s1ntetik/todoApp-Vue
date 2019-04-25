<template>
	<div class="btn-group">
		<button type="button"
				class="btn"
				value="all"
				@click="changeFilter"
				:class="{
				'btn-info': filter === 'all',
				'btn-outline-secondary': filter !== 'all' }">
			All
		</button>
		<button type="button"
				class="btn"
				value="active"
				@click="changeFilter"
				:class="{
				'btn-info': filter === 'active',
				'btn-outline-secondary': filter !== 'active' }">
			Active
		</button>
		<button type="button"
				class="btn"
				value="done"
				@click="changeFilter"
				:class="{
				'btn-info': filter === 'done',
				'btn-outline-secondary': filter !== 'done' }">
			Done
		</button>
	</div>
</template>

<script>
  export default {
    name: 'ItemStatusFilter',
    props: ['filter'],
    mounted() {

    },
	methods:{
      changeFilter(e){
        this.$emit('filter', e.target.value)
      }
	}
  }
</script>

<style>

</style>