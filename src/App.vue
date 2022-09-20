<template>
  <div class="content">
    <h1>To-Do List</h1>
    <form @submit.prevent="addTodo">
      <div class="field">
      <label class="label">Todo</label>
      <div class="control">
        <input v-model="todo" type="text" class="input" placeholder="Add" >
      </div>
    </div>
    <button type="submit" class="button is-warning">Add</button>
    </form>

    <div v-for="todo in todos" :key="todo.id" class="card my-5 mx-5">
      <div class="card-content">
        <div class="media">
          <div class="media-left"></div>
          <div class="media-content ">
            <p :class="{ done: todo.done }" @click="done(todo)" class="title is-4 cursor" >{{todo.content}}</p>
            <p class="sobtitle is-6">Done: {{ todo.done}}</p>
          </div>
        </div>
      </div>
    </div>  
  </div>
</template>

<script>
import { ref } from "vue"
export default {
  setup() {
    let todo = ref('')
    let todos = ref([]);

    function addTodo  () {
      todos.value.push({
        done: false,
        content: todo.value,
        id:Date.now(),
      }) 
      todo.value=""
    }
    function done (todo){
      todo.done = !todo.done
    }
    return {
      todo,
      todos,
      addTodo,
      done,
    }
  }
}
</script>
<style lang="scss">
  .content{
   text-align: center;
  }
  .input {
    width: 80% !important;
    height: 65px !important;
  }
  .cursor{
    cursor: pointer;
  }
  .done{
    text-decoration: line-through;
  }
  .card-content{
    border-radius: 20px;
    box-shadow: 3px 3px 4px #000!important;
  }
</style>
