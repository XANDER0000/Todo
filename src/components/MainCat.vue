<template>
<div class="nav__wrapper">
  <div tabindex="0" v-for="category in cat_data" :key="category.id" @click="selectedCat(category)"  class="nav__item" :class="{active : category.clicked == true}">{{ category.name }}</div>
</div>
</template>

<script>
export default {
  name: 'MainCat',

  data: () => ({

 }),

  props: {
    cat_data: {
      type: Object,
      default() {
        return {}
      }
    },
  },

  methods: {
    selectedCat(category) {
      this.$emit('select', category)
    },
  },

}
</script>

<style scoped lang="less">
  .nav__wrapper {
    display: flex;
    margin: 20px 0 35px 0;
    justify-content: center;
  }

  .nav__item {
    cursor: pointer;
    font-size: 17px;
    position: relative;
    margin: 0 20px 0 0;
    padding: 0 10px 0 0;
    transition: all .2s ease;

    &:focus {
      color: #fff;

      &::before {
        width: 100%;
      }
    }

    &:hover {
      color: #fff;

      &::before {
        width: 100%;
      }
    }

    &:last-child {
      margin: 0;
    }

    &::before {
      position: absolute;
      content: '';
      background: #5fc9c9;
      width: 0%;
      height: 1.5px;
      left: -5px;
      top: 49%;
      transition: width .3s ease-in-out ;
    }

    &.active {
      color: #fff;

      &::before {
        width: 100%;
      }
    }
  }
</style>
