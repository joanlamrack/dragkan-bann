<template>
  <div id="app">
	  <Navbar @new-task="addNewTask"></Navbar>
	  <div v-if="!(Object.keys(data)!==0)">
		  Loading.....
	  </div>
	  <div class="row" v-else>
		  <List :kanbandata="data.Todo" @move-after="moveTask" @move-previous="moveTask" :kanbantitle="'Todo'"></List>
		  <List :kanbandata="data.Doing" @move-after="moveTask" @move-previous="moveTask" :kanbantitle="'Doing'"></List>
		  <List :kanbandata="data.Done" @move-after="moveTask" @move-previous="moveTask" :kanbantitle="'Done'"></List>
	  </div>
	  
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import List from "./components/List.vue"
import { db } from './firebase.js'
import { functions } from 'firebase';
import Navbar from "./components/Navbar.vue";

export default {
  name: 'app',
  components: {
	HelloWorld,
	List,
	Navbar
  },
  data(){
	  return{
		  data:{}
	  }
  },
  methods:{
	  addNewTask:function(val){
		   if(this.data.Todo.list){
			  this.data.Todo.list.push(val);
		  }
		  else{
			  this.data.Todo.list = [];
			  this.data.Todo.list.push(val);

		  }
		  this.updatedata();
	  },
	  moveTask:function({index, from, destination}){
		  console.log(index, from, destination);
		  let movedTask = this.data[from].list.splice(index,1);
		  if(this.data[destination].list){
			  this.data[destination].list.push(movedTask[0]);
		  }
		  else{
			  this.data[destination].list = [];
			  this.data[destination].list.push(movedTask[0]);

		  }
		  this.updatedata();
	  },
	  updatedata:function(){
		  db.ref(`/`).set(this.data)
	  }
  },
  mounted(){
	  let self=this
	db.ref(`/`).on('value', function (snapshot) {
      let value = snapshot.val()
	  console.log(value)
	  self.data=value
    })
  }
}
</script>

<style>
</style>
