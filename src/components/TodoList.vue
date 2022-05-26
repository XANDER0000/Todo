<template>
<div class="list">
 <div class="list__wrapper">
   <transition-group name="list">
   <todo-item
    v-for="todo in todo_data"
    :key="todo.id"
    :todo_data="todo"
    @remove="$emit('remove', todo)"
    @complete="$emit('complete', todo)"
   />
   </transition-group>
  </div>
</div>
</template>

<script>
import TodoItem from '@/components/TodoItem.vue'
export default {
 name: 'TodoList',
 components: {
  TodoItem,
 },

  data: () => ({

 }),

 props: {
  todo_data: {
   type: Object,
   default() {
    return {}
   }
  },
 },

 methods: {

 }
}
</script>

<style lang="less">
.list {
 padding: 30px 0;
}

.list__wrapper {
 width: 100%;
 max-width: 1000px;
 margin: 0 auto;
 padding: 0 10px;
}

.list-enter-active, .list-leave-active {
  transition: all .2s ease;
}
.list-enter-from, .list-leave-to  {
  opacity: 0;
  transform: translateX(130px);
}
</style>