<template>
  <div id="app">
    <h1 v-text='title'></h1>
    <input v-model="newItem" v-on:keyup.enter="addNew()"/>
    <ul>
    	<li v-for='item in items' v-bind:class="{finish:item.isFinished}" v-on:click="togglefinish(item)">
    	{{item.label}}
    	</li>
    </ul>
  </div>
</template>

<script>
import Store from './store.js'

export default {
  data: function(){
  	return {
  		title:'this is a todo list',
  		items:(Store.fetch()===null?new Array():Store.fetch()),
  		liclass:'this is liclass',
  		newItem:''
  		
  	}
  },
  methods:{
  	togglefinish:function(item){
  			item.isFinished=!item.isFinished
  	},
  	addNew:function(){
      console.log(this.items)
  		this.items.push({
  			label:this.newItem,
  			isFinished:false
  		})
  		this.newItem = ' ';
//		this.item.label=thisNewitem
//		this.item.isFinished=false;
  	}
  },
  watch:{
  	items:{
  		handler:function(items){
  			Store.save(items)
  		}
  		
  	}
  }
}
</script>

<style>
	li{
		list-style: none;
		cursor: pointer;
	}
.finish{
		text-decoration: line-through;
	}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
