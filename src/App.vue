<template>
  <div id="app">
    <TodoList :items="sortedItem" @onItemDone="done" />
    <InputForm @onSave="save" />  
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
import InputForm from "@/components/InputForm";
import {mapState,mapMutations} from "vuex";

export default {
  name: "App",
  components:{
    TodoList,
    InputForm
  },
  mounted(){
    this.initItem(JSON.parse(localStorage.getItem('todoItem')))
  },
  computed: {
    ...mapState(['items']),
    sortedItem() {
      return [...this.items]
        .sort((a, b) => b.time - a.time)
        .filter((ele) => ele.completed === false);
    },
  },
  methods: {
    ...mapMutations(['addItem','initItem']),
    done(time) {
      this.items.map((item) => {
        if (time === item.time) {
          item.completed = true;
        }
        return item;
      });
    },
    save(text) {
      this.addItem({
        text: text,
        time: Date.now(),
        completed: false,
      });
      this.initItem(this.items)
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
