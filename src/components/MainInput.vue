<template>
<div class="search__wrapper">
 <input @keyup.enter ="makeNewTodo(todoValue)" v-model="todoValue" autofocus class="search__input" placeholder="Name of the Task" type="text">
 <button @click="makeNewTodo(todoValue)" class="btn">Add new ToDo</button>
</div>

</template>

<script>
export default {
 name: 'MainSearch',

 data: () => ({
  todoValue: '',
 }),

 methods: {
    makeNewTodo(todoValue) {
     this.$emit('makeNewTodo', todoValue);
     this.todoValue =  '';
   },
  }
}
</script>

<style lang="less" scoped>
.search__wrapper {
 display: flex;
 justify-content: center;
 margin-top: 30px;

  .btn {
     @media (max-width: 480px) {
      font-size: 15px;
      max-width: 150px;
      margin: 16px 0;
    }
  }

   @media (max-width: 480px) {
     flex-direction: column;
     align-items: center;
    }
}

.search__input {
 border: 0;
 border-radius: 2px;
 margin-right: 7px;
 padding: 0 0 0 10px;
 font-size: 17px;
 letter-spacing: .6px;
 outline: none;
 width: 500px;
 background: #e1e1e1;

 &:focus {
  border: 1.5px solid #5fc9c9;
  -webkit-box-shadow: 0px 0px 11px 4px rgba(95, 201, 201, 0.23);
  -moz-box-shadow: 0px 0px 11px 4px rgba(95, 201, 201, 0.23);
  box-shadow: 0px 0px 11px 4px rgba(95, 201, 201, 0.23);
 }

 @media (max-width: 680px) {
   width: 400px;
 }

  @media (max-width: 590px) {
   width: 300px;
 }

  @media (max-width: 480px) {
     margin: 0;
     height: 40px;
     width: 100%;
    }
}
</style>