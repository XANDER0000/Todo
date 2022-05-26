<template>
<div class="container">
  <main-input @click.prevent @makeNewTodo="makeNewTodo"/>
  <main-cat @select='selectedCat'  :cat_data="categories"/>
  <todo-list @complete='doComplete' @remove='removeTodo' :todo_data="filteredTodos"/>
</div>
</template>

<script>
import MainCat from '@/components/MainCat.vue'
import MainInput from '@/components/MainInput.vue'
import TodoList from '@/components/TodoList.vue'


export default({
  components: {
    MainCat, MainInput, TodoList
  },
  data: () => ({
    newTodoid: 3,
    sortedTodos: [],
    flag_rewrite: false,

   todos: [
    {
     id: 1,
     name: 'Take over the world!',
     completed: 'Active'
    },

    {
     id: 2,
     name: '....',
     completed: 'Completed'
    },

     {
     id: 3,
     name: 'PROFIT',
     completed: 'Active'
    },

   ],

   categories: [
       {
           id: 1,
           name: 'All',
           clicked: true,
       },
       {
           id: 2,
           name: 'Completed',
           clicked: false,
       },
       {
           id: 3,
           name: 'Active',
           clicked: false,
       },
   ],
 }),

 mounted() {
    if (localStorage.getItem('todos')) {
      try {
        this.todos = JSON.parse(localStorage.getItem('todos'));
      } catch(e) {
        localStorage.removeItem('todos');
      }
    }
  },



 methods: {
     makeNewTodo(todoValue) {
        if (todoValue.length > 0) {
            const newTodo = {
                name: todoValue,
                id: this.newTodoid++,
                completed: 'Active',
            };
        this.todos.push(newTodo);
        this.saveTodos()
        }

     },

     removeTodo(todo) {
        this.todos = this.todos.filter(t => t.id !== todo.id)
        this.sortedTodos = this.sortedTodos.filter(t => t.id !== todo.id)
        this.saveTodos()
    },

    saveTodos() {
      const parsed = JSON.stringify(this.todos);
      localStorage.setItem('todos', parsed);
    },

    selectedCat(category) {
         this.sortedTodos = [];
         this.categories.forEach(item => {
            item.clicked = false
        })

         category.clicked = ! category.clicked
            let vm = this;
            this.todos.map(function (item) {
                if (item.completed === category.name) {
                    vm.sortedTodos.push(item)
                }
            })
    },

    doComplete(todo) {
        if (todo.completed == 'Completed') {
            todo.completed = 'Active'
        } else {
            todo.completed = 'Completed'
        }
         this.saveTodos()
    }
 },

 computed: {
        filteredTodos() {
            if (this.sortedTodos.length) {
                return this.sortedTodos
            } else {
               return this.todos
            }
        },
    },
})
</script>


<style lang="less">

.container {
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 10px;
}

@black: #444;
@blue: #1D46F6;
@white: #fff;


body {
    margin: 0;
    position: relative;
    height: 100%;

    font-family: 'Work Sans', sans-serif;

    font-size: 15px;
    background: #252525;
    color: #adadad;
    -webkit-font-smoothing: antialiased;

    &.no-scroll {
        overflow: hidden;
    }
}

ul {
    padding: 0;
}

.wrapper {
    min-height: 100%;
    display: flex;
    flex-direction: column;
    flex: 1 1 auto;
}

h1, h2, h3, h4, h4, h5 {
    margin: 0;
}

*,
*:before,
*:after {
    box-sizing: border-box;
}

.btn {
    display: flex;
    flex-direction: row;
    position: relative;
    align-items: center;
    justify-content: center;

    padding: 8px 13px;

    font-size: 18px;
    line-height: 123.6%;
    font-family: 'Work Sans', sans-serif;
    font-weight: 400;
    z-index: 10;
    color: #adadad;
    text-decoration: none;
    background: none;
    border: 1px #adadad solid;
    border-radius: 2px;
    cursor: pointer;

    background-color: transparent;


    transition: all .2s ease-out, transform .1s ease-in;

    &:focus {
        outline: none;
    }

    &:hover {
      transition: box-shadow .2s ease .3s;
      -webkit-box-shadow: 0px 0px 11px 4px rgba(95, 201, 201, 0.23);
      -moz-box-shadow: 0px 0px 11px 4px rgba(95, 201, 201, 0.23);
      box-shadow: 0px 0px 11px 4px rgba(95, 201, 201, 0.23);
      color: #fff;
      border-color: #5fc9c9;
    }

    &:active {
        filter: drop-shadow(4px 5px 15px rgba(#1D46F6, 0.4));

        transform: scale(.94);
    }
}


</style>
