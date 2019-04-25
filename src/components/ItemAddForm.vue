<template>
	<form
		class="item-add-form d-flex"
		@submit="addItem">
		<input v-model="itemName" type="text" class="form-control" placeholder="What needs to be done"/>
		<button class='btn btn-outline-secondary'>
			Add Item
		</button>
	</form>
</template>

<script>
  export default {
    name: "ItemAddForm",
	data(){
      return{
        itemName: ''
	  }
	},
	methods:{
      addItem(e){
        e.preventDefault();
		this.$emit('addItem', this.itemName);
		this.itemName = ''
	  }
	}
  }
</script>

<style scoped>
	.item-add-form {
		margin: 0.5rem 0;
	}

	.item-add-form input{
		margin-right: 3px;
	}

	.item-add-form button{
		white-space: nowrap;
	}
</style>