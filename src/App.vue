<template>
  <div id="app">
    <div class="vueContainer vueContainer-Container">
      <div class="inner">
        <div>
          <h1 class="header">TVU Network Demo</h1>

            <div class="my-4 container">
              <div class="row">
                <div class="col-sm-8">
                  <div class="row">
                    <div class="col-sm-8">
                      <sceneItems v-for="vueContainer in list" 
                      :vueContainer="vueContainer" 
                      @delete="onDeleteItem"
                      :key="vueContainer.id" />
                    </div>
                    <div class="col-sm-4"><img src={this.logo} /></div>
                  </div>
                </div>
                <div class="col-sm-4">
                  <storyList v-for="vueContainer in list" 
                  :vueContainer="vueContainer" 
                  @delete="onDeleteItem"
                  :key="vueContainer.id" />
                </div>
              </div>

              <div class="row">
                <div class="thumbnailAdd col-12">
                  <div><input type="text" v-model="vueContainer" v-on:keyup.enter="createNewstoryList"/></div>
                  <button @click="createNewstoryList()">Add</button>
                </div>
              </div>
            
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import storyList from './components/storyList.vue'
import sceneItems from './components/sceneItems.vue'
import Logo from './assets/logo.png';
import axios from 'axios';

export default {
  name: 'vueContainer',
  components: {
    storyList,
    sceneItems
  },
  created () {
      this.getPosts()
  },
  data() {
      return {
          list: [],
          vueContainer: '',
          logo: Logo
      }
  },
  methods: {
      getPosts () {
         axios({
            method: 'GET',
            url: 'http://localhost:3000/list/'
          }).then((res)=>{
            console.log("resGET1>>>", res)
            this.list = res.data
            console.log("resGET2>>>", this.list)
          })
      },
      createNewstoryList() {
        //validate vueContainer
        if (!this.vueContainer){
          alert("Please enter a vueContainer!");
          return
        }

        var self=this;
        const newId = Math.max.apply(null, this.list.map(t => t.id)) + 1;
        console.log("newId>>>", newId)
        axios.post('http://localhost:3000/list/', { id: newId, text: this.vueContainer})
        .then((response) => {
          self.getPosts();
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
        });
        
        
        this.vueContainer = '';
      },
      onDeleteItem(vueContainer){
       
        var self=this;
        axios({
          method: 'DELETE',
          url: 'http://localhost:3000/list/'+vueContainer.id,
          headers: { 'Content-Type': 'application/json' },
        }).then((res)=>{
            self.getPosts();
        });

        // this.list = this.list.filter(item => item !== vueContainer);
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

  .vueContainer {
    border: 1px solid white;
    width: 100%;
    max-width: 1000px;
    height: auto;
    display:table;
    margin:0 auto;
    margin-top: 50px;
  }
  .vueContainer .inner{ display: table-cell; width: 100%; height: 100%; vertical-align: middle;}

  .header {
    color: black;
    font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica, Arial, sans-serif;
    font-weight: 400;
    background-color: #de4843;
    color: #fff;
    font-size:22px;
    padding: 12px 10px;
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
  .thumbnailAdd { display: table; width: 100%; }
  .thumbnailAdd div { display: table-cell; width: 100%; }
  .thumbnailAdd button {
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

  .vueContainer-Container {
    margin: 0 auto;
    /* padding: 35px 25px 0 25px; */
    border: 1px solid #b7b4b4;
    background: #f6f6f6;
    border-top:0; 
    margin-top: 40px;
  }
  /* .vueContainer-Content{ margin-top: 35px; margin-bottom:35px; } */

  
</style>
