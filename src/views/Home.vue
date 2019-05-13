<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" /> <!-- todos data를 넘겨주기 (pros로 넘어감) -->
  </div>
</template>

<script>
import axios from 'axios' // HTTP를 통해 REST API에 요청을 보내기 위해 사용
import Todos from '../components/Todos'; //todos component import로 가져오기
// import Header from '../components/layout/Header'; App.vue로 옮김
import AddTodo from '../components/AddTodo';
export default {
  name: 'app',
  components: {
    Todos, //위에서 import로 가져온 component 선언하기
    // Header, App.vue로 옮김
    AddTodo
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "Todo One",
          completed: false
        },
        {
          id: 2,
          title: "Todo Two",
          completed: true
        },
        {
          id: 3,
          title: "Todo Three",
          completed: false
        }

      ]        
    }
  },
  methods: {
    deleteTodo(id) {
      axios.delete("https://jsonplaceholder.typicode.com/todos/${id}")
      .then(res =>  this.todos = this.todos.filter(todo => todo.id !== id))
      .catch(errorMsg => console.log(errorMsg));
    },
    addTodo(newTodo) {
      const {title, completed} = newTodo;

      axios.post("https://jsonplaceholder.typicode.com/todos", {
        title,
        completed
      })
      .then(res => this.todos = [...this.todos, res.data])
      .catch(er0roMsg => console.log(errorMsg));
    }
  },
  created() { //component가 로드될 때 불림 (init 역할)
    axios.get("https://jsonplaceholder.typicode.com/todos?_limit=5") //200개를 불러오면 너무 많으니까 5개만 불러오도록 limit 설정
      .then(res => this.todos = res.data)
      .catch(errorMsg => console.log(errorMsg));
  }

}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
