<template>
	<input
		v-model="searchInput"
		@input="onSearch"
		type="text"
		class="form-control search-input"
		placeholder="type to search"/>
</template>

<script>
  export default {
    name: 'SearchPanel',
	data(){
      return{
        searchInput: ''
	  }
	},
	methods:{
      onSearch(){
        this.$emit('onSearch', this.searchInput)
      }
	}
  }

</script>

<style>
.search-input {
	width: auto;
	flex-grow: 1;
	margin-right: 3px;
}
</style>