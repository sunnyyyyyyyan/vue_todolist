<template>
  <div id="app">
    <img src="./assets/logo.png" width="100px" >
    <h1>{{title}}</h1>
    <div class="container">
      <input type="text" placeholder="enter" v-model="newItem" v-on:keyup.enter="addItem">
      <ul>
        <li v-for="(item,index) in items" v-bind:class="{active : item.isActive}" v-on:click="deleteItem(index)">{{index}}-{{item.label}}</li>
      </ul>
    </div>

  </div>
</template>

<script>
import Store from './store'
//console.log(Store);
export default {
  name: 'App',
  data(){
    return{
      title:'todo list',
      items:Store.fetch(),
      /*[
        /!*{ label:'sunny',isActive:false },
        { label:'sunny',isActive:true }*!/
      ],*/
      newItem:''
    }
  },
  watch:{
    items:{
      /*handler(val,oldVal){
        console.log(val, oldVal);
      },*/
      handler(items){
        Store.save(items);
      },
      deep:true
    }
  },
  methods:{
    toggleActive(item){
      //console.log(item);
      item.isActive != item.isActive;
      console.log(item);
    },
    addItem(){                    //添加元素

      this.items.push({
        label:this.newItem,
        isActive:false
      });
      //console.log(this.newItem);
      this.newItem = '';
      Store.save(this.items);
    },
    deleteItem(index){               //点击删除
      this.items.splice(index,1);
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

  .active{
    text-decoration: underline;
  }

  li{
    list-style: none;
  }
</style>
