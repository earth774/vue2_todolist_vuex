<template>
  <div class="todo-list">
    <ul>
      <li v-for="item in items" :key="item.time">
        <button @click="itemDone(item.time)">Done</button> {{ item.text | capitalize}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name:"TodoList",
  props:{
    items:{
      type:Array
    }
  },
  filters:{
    capitalize(val){
      return val.toUpperCase();
    }
  },
  methods:{
    itemDone(time){
      this.$emit('onItemDone',time);
    }
  }
}
</script>

<style lang="scss" scoped>

</style>