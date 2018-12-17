<template>
  <div id="app">
    <div class="ToDo">
      <div class="inner">
        <div>
          <h1 class="ToDo-Header">Demo</h1>
          <div class="ToDo-Container">
            <div class="ToDo-Add">
              <div><input type="text" v-model="todo" v-on:keyup.enter="createNewToDoItem"/></div>
              <button @click="createNewToDoItem()">Add</button>
            </div>
            <div class="ToDo-Content">
              <ToDoItem v-for="todo in list" 
                        :todo="todo" 
                        @delete="onDeleteItem"
                        :key="todo.id" />
            </div>
            
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ToDoItem from './components/ToDoItem.vue'
import Logo from './assets/logo.png';

export default {
  name: 'to-do',
  components: {
    ToDoItem
  },
  data() {
      return {
          list: [
              {
                id: 1,
                text: 'Add detail 1'
              },
              {
                id: 2,
                text: 'Add detail 2'
              }
          ],
          todo: '',
          logo: Logo
      }
  },

  methods: {
      createNewToDoItem() {
        //validate todo
        if (!this.todo){
          alert("Please enter a todo!");
          return
        }

        const newId = Math.max.apply(null, this.list.map(t => t.id)) + 1;
        this.list.push({ id: newId, text: this.todo});
        this.todo = '';
      },
      onDeleteItem(todo){
        this.list = this.list.filter(item => item !== todo);
      }

  },
}
</script>

<style>

  body {
    margin: 0;
    padding: 0;
    font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica, Arial, sans-serif;
    height: auto;
    justify-content: center;
    align-items: center;
    font-size: 15px;
  }
  h1, p{ margin: 0; padding: 0;}

  .Logo {
    width: 50px;
    position: relative;
    top: 50px;
  }

  .ToDo {
    border: 1px solid white;
    width: 100%;
    max-width: 700px;
    height: 100vh;
    display:table;
    margin:0 auto;
  }
  .ToDo .inner{ display: table-cell; width: 100%; height: 100%; vertical-align: middle;}

  .ToDo-Header {
    color: black;
    font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica, Arial, sans-serif;
    font-weight: 400;
    background-color: #de4843;
    color: #fff;
    font-size:22px;
    padding: 12px 10px;
    text-align: center;
  }
  input {
    width: 100%;
    padding: 10px;
    font-size: 14px;
    box-shadow: none;
    border: 1px solid #adadad;
    border-right: 0;
    outline:0;
  }
  input:hover, input:focus, input:Active{ outline: 0; }
  .ToDo-Add { display: table; width: 100%; }
  .ToDo-Add div { display: table-cell; width: 100%; }
  .ToDo-Add button {
    color: white;
    font-size: 14px;
    padding: 11px;
    cursor: pointer;
    background: #de4843;
    border-radius: 0px;
    display: table-cell;
    width:100px;
    box-shadow:none;
    border: 0;
  }

  .ToDo-Container {
    margin: 0 auto;
    padding: 35px 25px 0 25px;
    border: 1px solid #b7b4b4;
    background: #f6f6f6;
    border-top:0; 
  }
  .ToDo-Content{ margin-top: 35px; margin-bottom:35px; }

  
</style>
