<template>
	<div class="todo-app">
		<AppHeader :count="todoCount"/>
		<div class="top-panel d-flex">
			<SearchPanel @onSearch="onSearch"/>
			<ItemStatusFilter
					:filter="filter"
					@filter="onFilter"/>
		</div>
		<TodoList
				:todoData="visibleItems"
				@toParentEvent="onGetEvent"/>
		<ItemAddForm
				@addItem="addItem"/>
	</div>
</template>

<script>
  import AppHeader from './components/AppHeader.vue'
  import SearchPanel from './components/SearchPanel.vue'
  import ItemStatusFilter from './components/ItemStatusFilter.vue'
  import TodoList from './components/TodoList.vue'
  import ItemAddForm from './components/ItemAddForm.vue'

  export default {
    name: 'app',
    components: {
      AppHeader,
      SearchPanel,
      ItemStatusFilter,
      TodoList,
      ItemAddForm
    },
    data() {
      return {
        itemId: 1,
        todoData: [],
        searchText: '',
        filter: 'all'
      }
    },
    mounted() {
      this.todoData = [
        this.createTodoItem('Drink Coffee'),
        this.createTodoItem('Make Awesome App'),
        this.createTodoItem('Have a lunch'),
      ]
    },
    methods: {
      createTodoItem(label) {
        return {
          label: label,
          important: false,
          done: false,
          id: this.itemId++
        };
      },

      onFilter(value) {
        this.filter = value;
      },

      onGetEvent(id, nameProps) {
        const idx = this.todoData.findIndex((item) => item.id === id);

        if (nameProps === 'delete') {
          this.$delete(this.todoData, idx);
        } else {
          this.todoData[idx][nameProps] = !this.todoData[idx][nameProps]
        }
      },

      addItem(itemName) {

        const newItem = this.createTodoItem(itemName);
        this.$set(this.todoData, this.todoData.length++, newItem)
      },

      onSearch(searchText) {
        this.searchText = searchText
      },

      filterItems(items, filter) {
        switch (filter) {
          case 'all':
            return items;
          case 'active':
            return items.filter((item) => !item.done)
          case 'done':
            return items.filter((item) => item.done)
          default:
            return items
        }
      }
    },
    computed: {
      visibleItems() {
        const visibleItems = this.todoData.filter((item) => {
          return item.label.toLowerCase().indexOf(this.searchText.toLowerCase()) > -1
        });

        const filterItems = this.filterItems(visibleItems, this.filter)
        return filterItems;
      },
      todoCount() {
        const doneCount = this.todoData.filter((el) => el.done).length;
        const todoCount = this.todoData.length - doneCount;

        return {
          todoCount,
          doneCount
        }
      },
    }
  }
</script>

<style>
	.todo-app {
		margin: 2rem auto 0 auto;
		max-width: 400px;
	}

	.top-panel {
		margin: 1rem 0;
	}


</style>
