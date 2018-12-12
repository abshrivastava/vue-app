<template>
  <div id="app">
    <div class="ToDo">
      <!-- <img class="Logo" :src="logo" alt="Vue logo"> -->
      <h1 class="ToDo-Header">Welcome !!!</h1>
      <div class="ToDo-Container">
        <!-- <div class="ToDo-Content">
          <ToDoItem v-for="todo in list" :todo="todo" @delete="onDeleteItem" :key="todo.id"/>
        </div>-->
        <!-- <input type="text" v-model="todo" v-on:keyup.enter="createNewToDoItem"> -->
        <!-- <div class="ToDo-Add" @click="createNewToDoItem()">+</div> -->
      </div>
    </div>
    <div class="container">
      <h1 class="display-4 mb-4">Fetching API Data</h1>
      <div class="d-flex">
        <!-- <button class="btn btn-primary mr-4" @click="getText()" id="getText">Get Text</button> -->
        <!-- <button class="btn btn-success mr-4" @click="getUsers()" id="getUsers">Get JSON</button>
        <button class="btn btn-warning mr-4" @click="getPosts()" id="getPosts">Get API DATA</button>-->
        <div v-for="post in posts" :key="post.id">
          <h3>{{ post.title }}</h3>
        </div>
      </div>
      <hr>
      <div id="output"></div>
      <!-- <form id="addPost">
        <div class="form-group">
          <input type="text" id="title" class="form-control" placeholder="Title">
        </div>
        <div class="form-group">
          <textarea id="body" class="form-control" placeholder="Body"></textarea>
        </div>
        <input type="submit" class="btn btn-secondary" value="Submit">
      </form>-->
    </div>
  </div>
</template>

<script>
import ToDoItem from "./components/ToDoItem.vue";
// import Logo from "./assets/logo.png";

// const API_KEY = "a5774b19c0bb713704ac27aad1764191";

// document.getElementById('getText').addEventListener('click', getText);
// document.getElementById('getUsers').addEventListener('click', getUsers);
// document.getElementById('getPosts').addEventListener('click', getPosts);
// document.getElementById('addPost').addEventListener('submit', addPost);

// function getUsers(){
//   fetch('users.json')
//   .then((res) => res.json())
//   .then((data) => {
//     let output = '<h2 class="mb-4">Users</h2>';
//     data.forEach(function(user){
//       output += `
//         <ul class="list-group mb-3">
//           <li class="list-group-item">ID: ${user.id}</li>
//           <li class="list-group-item">Name: ${user.name}</li>
//           <li class="list-group-item">Email: ${user.email}</li>
//         </ul>
//       `;
//     });
//     document.getElementById('output').innerHTML = output;
//   })
// }

// function getPosts(){
//   fetch('https://jsonplaceholder.typicode.com/posts')
//   .then((res) => res.json())
//   .then((data) => {
//     let output = '<h2 class="mb-4">Posts</h2>';
//     data.forEach(function(post){
//       output += `
//         <div class="card card-body mb-3">
//           <h3>${post.title}</h3>
//           <p>${post.body}</p>
//         </div>
//       `;
//     });
//     document.getElementById('output').innerHTML = output;
//   })
// }

// function addPost(e){
//   e.preventDefault();

//   let title = document.getElementById('title').value;
//   let body = document.getElementById('body').value;

//   fetch('https://jsonplaceholder.typicode.com/posts', {
//     method:'POST',
//     headers: {
//       'Accept': 'application/json, text/plain, */*',
//       'Content-type':'application/json'
//     },
//     body:JSON.stringify({title:title, body:body})
//   })
//   .then((res) => res.json())
//   .then((data) => console.log(data))
// }
import axios from "axios";
export default {
  data() {
    return {
      id: "",
      title: ""
    };
  },
  mounted() {
    axios({
      method: "GET",
      url: "https://jsonplaceholder.typicode.com/posts"
    }).then(
      result => {
        //  posts = result.data
        console.log("result:", result.data[11]);
        document.getElementById("output").innerHTML = result.data[11].body;
      },
      error => {
        console.error(error);
      }
    );
  }
  // methods: {
  //   sendData() {
  //     axios({
  //       method: "POST",
  //       url: "https://jsonplaceholder.typicode.com/posts",
  //       data: this.input,
  //       headers: { "content-type": "application/json" }
  //     }).then(
  //       result => {
  //         this.response = result.data;
  //       },
  //       error => {
  //         console.error(error);
  //       }
  //     );
  //   }
  // }
  //   name: "to-do",
  //   components: {
  //     ToDoItem
  //   },
  //   data() {
  //     return {
  //       list: [
  //         {
  //           id: 1,
  //           text: "clean the house"
  //         },
  //         {
  //           id: 2,
  //           text: "buy milk"
  //         }
  //       ],
  //       todo: "",
  //       logo: Logo
  //     };
  //   },

  // methods: {
  //   createNewToDoItem() {
  //     if (!this.todo) {
  //       alert("Please enter a todo!");
  //       return;
  //     }

  //     const newId = Math.max.apply(null, this.list.map(t => t.id)) + 1;
  //     this.list.push({ id: newId, text: this.todo });
  //     this.todo = "";
  //   },
  //   onDeleteItem(todo) {
  //     this.list = this.list.filter(item => item !== todo);
  //   },

  //   getText() {
  //     alert("Connected...");
  //     this.$http.get(`http://api.openweathermap.org/data/2.5/forecast?id=1271308&appid=${API_KEY}`)
  //       .then(res => {
  //         console.log("res1111>>>>", res);
  //         console.log(res.headers.get("Content-Type"));
  //         console.log(res.headers.get("Date"));
  //         res.text();
  //         console.log("res2222>>>>", res.text());
  //       })
  //       .then(data => {
  //         console.log("data>>>", data);
  //         document.getElementById("output").innerHTML = data;
  //       })
  //       .catch(err => console.log(err));
  //   }
  // }
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
  font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica,
    Arial, sans-serif;
  background: linear-gradient(#aeffae, #3d99ff);
  height: auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* .Logo {
  width: 50px;
  position: relative;
  top: 50px;
} */

.ToDo {
  text-align: center;
  border: 1px solid white;
  width: 80vw;
  height: auto;
  box-shadow: 2px 3px 15px rgba(0, 0, 0, 0.5);
  background: #f6f6f6;
  padding-bottom: 60px;
  margin: 40px auto;
}

.ToDo-Header {
  color: black;
  font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica,
    Arial, sans-serif;
  font-weight: 400;
  text-transform: uppercase;
  margin: 70px auto 30px;
}

.ToDo-Add {
  color: white;
  font-size: 2em;
  width: 1.5em;
  height: 0.3em;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  cursor: pointer;
  background: #73ff73;
  border-radius: 10px;
  box-shadow: 1px 1px 1px #47a947;
  margin: 20px auto 0;
}

.ToDo-Add:hover {
  box-shadow: none;
  margin-top: 21px;
  margin-left: calc(auto + 1px);
}

.ToDo-Container {
  width: 80%;
  margin: 0 auto;
}

input {
  width: 60%;
  padding: 10px;
  font-size: 1em;
  margin: 10px auto;
  box-shadow: 1px 3px 20px 0px rgba(0, 0, 0, 0.3);
}
</style>
