<template>
  <div id="app" class="main">
    
    <div class="main__control control">
      <AddTodo
        @add-item="addItem"
        @remove-items="removeItems"
        @filter-items="filterItems"
     
      />
       <h2>Поиск по списку</h2>
      <input class="control__input" type="text" v-model="search">
    </div>
    <Loader v-if="loading" />
    <TodoList
      v-else-if="items.length"
      v-bind:items="searchHandler" 
      @remove-item="removeItem" 
    />
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
import AddTodo from "@/components/AddTodo";
import Loader from "@/components/Loader";

export default {
  name: "App",
  data() {
    return {
      items: [],
      search: '',
      loading: true,
    };
  },
  components: {
    TodoList,
    AddTodo,
    Loader,
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then((response) => response.json())
      .then((json) => {
        setTimeout(() => {
          this.items = json;
          this.loading=false;
        }, 3000);
      });
  },
  computed: {
    searchHandler() {
      return this.items.filter((i) => {
        return i.title.toLowerCase().indexOf(this.search) !== -1;
      });
    },
  },
  methods: {
    removeItem(id) {
      this.items = this.items.filter((i) => i.id !== id);
    },
    removeItems() {
      this.items = this.items.filter((i) => i.completed !== true);
    },
    addItem(item) {
      this.items.push(item);
    },
    filterItems() {
      this.items.sort((a, b) => a.title.localeCompare(b.title));
    },
  },
};
</script>

<style lang="scss">
$bg: #373737;

body {
  background: $bg;
  margin: 0;
  padding: 0;
  font-size: 12px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: white;
  margin-top: 60px;
}
.main {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  position: relative;
  margin: 1%;

  .main__control {
    flex: 1 1 30%;
    margin: 0 2.5%;
  }
  .main__todo {
    flex: 1 1 60%;
  }
  h2 {
    text-align: center;
    margin: 0;
    padding: 0.5rem 0;
    font-size: 1.1em;
    position: relative;
    display: inline-block;
  }
  h2:before {
    content: "";
    position: absolute;
    bottom: 0.65rem;
    left: 1%;
    width: 98%;
    box-shadow: 1px 1px 2px 2px rgba(89, 119, 253, 0.6);
    height: .5px;
    background: #ccc;
    z-index: -1;
  }
}
</style>
