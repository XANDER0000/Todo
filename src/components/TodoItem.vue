<template>
<div :class="todoName">
 <div @click="$emit('complete', todo)" class="todo__name">
  {{ todo_data.name }}
 </div>
 <div>
    <div @click="$emit('remove', todo)" class="todo__delete"></div>
 </div>

</div>
</template>

<script>
export default {
 name: 'TodoItem',

 props: {
  todo_data: {
   type: Object,
   default() {
    return {}
   }
  },
 },

 computed: {
    todoName() {
      let classes = ['todo__item'];
      if (this.todo_data.completed == 'Completed') {
        classes.push('completed');
      }
      return classes.join(' ');
    }
  }
}
</script>

<style lang="less" scoped>
.todo__item {
 display: flex;
 justify-content: space-between;
 margin: 15px 0;
 border: 1.5px solid rgba(95, 201, 201, 0.553);
  -webkit-box-shadow: 0px 0px 10px 3px rgba(95, 201, 201, 0.17);
  -moz-box-shadow: 0px 0px 10px 3px rgba(95, 201, 201, 0.17);
  box-shadow: 0px 0px 10px 3px rgba(95, 201, 201, 0.17);

  &.completed {
   border: 1.5px solid rgba(201, 104, 95, 0.553);
  -webkit-box-shadow: 0px 0px 10px 3px rgba(201, 104, 95, 0.17);
  -moz-box-shadow: 0px 0px 10px 3px rgba(201, 104, 95, 0.17);
  box-shadow: 0px 0px 10px 3px rgba(201, 104, 95, 0.17);

    &:hover {
      border: 1.5px solid rgb(201, 104, 95);
      -webkit-box-shadow: 0px 0px 11px 4px rgba(201, 104, 95, 0.23);
      -moz-box-shadow: 0px 0px 11px 4px rgba(201, 104, 95, 0.23);
      box-shadow: 0px 0px 11px 4px rgba(201, 104, 95, 0.23);
    }
  }

  &:hover {
    background: rgba(23, 23, 23, 0.248);
    border: 1.5px solid #5fc9c9;
    -webkit-box-shadow: 0px 0px 11px 4px rgba(95, 201, 201, 0.23);
    -moz-box-shadow: 0px 0px 11px 4px rgba(95, 201, 201, 0.23);
    box-shadow: 0px 0px 11px 4px rgba(95, 201, 201, 0.23);
  }
}

.todo__name {
 cursor: pointer;
 word-wrap: break-word;
 font-size: 16px;
 line-height: 120%;
 letter-spacing: .78px;
 width: 100%;
 max-width: 907px;
 height: auto;
 padding: 15px;
 margin-right: 20px;

 @media (max-width: 680px) {
   margin-right: 0;
 }

 @media (max-width: 480px) {
   padding: 10px;
 }
}

.todo__delete {
 position: relative;
 width: 23px;
 height: 23px;
 margin: 15px;
 border: 1px rgba(173, 173, 173, .3) solid;
 border-radius: 100%;
 transition: all .2s ease-out, transform .1s ease-in;
 cursor: pointer;

 &::after {
   content: '';
   transform: rotate(45deg);
   position: absolute;
   width: 1.5px;
   height: 13px;
   left: 10px;
   top: 4px;
   background: #adadad;
 }

 &::before {
   content: '';
   transform: rotate(135deg);
   position: absolute;
   width: 1.5px;
   height: 13px;
   left: 10px;
   top: 4px;
   background: #adadad;
 }

  &:hover {
      transition: box-shadow .2s ease .3s;
      border-color: rgb(201, 104, 95);
      -webkit-box-shadow: 0px 0px 11px 4px rgba(201, 104, 95, 0.23);
      -moz-box-shadow: 0px 0px 11px 4px rgba(201, 104, 95, 0.23);
      box-shadow: 0px 0px 11px 4px rgba(201, 104, 95, 0.23);

      &::after, &::before {
        background: rgb(201, 104, 95);
      }
    }

  @media (max-width: 480px) {
   margin: 10px;
 }
}
</style>