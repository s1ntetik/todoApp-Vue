<template>
	<ul class="list-group todo-list">
		<li v-for="item in todoData" :key="item.id" class="list-group-item">
			<TodoListItem
					:item="item"
					@toParentEvent="toParentEvent"
			/>
		</li>
	</ul>
</template>

<script>
  import TodoListItem from '../components/TodoListItem'

  export default {
    name: 'TodoList',
    components: {
      TodoListItem
    },
    props: ['todoData'],
    methods: {
      toParentEvent(id, nameProps){
        this.$emit('toParentEvent', id, nameProps)
      }
    }
  }
</script>

<style>
	.todo-list .list-group-item {
		padding: .25rem .75rem;
	}
</style>