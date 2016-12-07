<template>
  <div class="todoList">
    <div class="title">{{msg}}</div>     
    <input type="text" v-model='newItem' v-on:keyup.enter='addNew' placeholder="请输入todo,enter添加">
    <div class="content">
      <ul>
        <li v-for="item in items" v-bind:class="{finished: item.isFinished }" v-on:click="toggleFinish(item)">
          {{item.labal}}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Store from '../store';
export default {
  name: 'todoList',
  data () {
    return {
      msg: 'Welcome to todoList',
      items:Store.fetch(),
      newItem:''
    }
  },
  watch:{
    items:{
      handler: function (items) { 
        Store.save(items);
      },
      deep:true
    }
  },
  methods:{
      toggleFinish:function(item){
        item.isFinished=!item.isFinished;
      },
      addNew:function(){
        this.items.push({
          labal:this.newItem,
          isFinished:false
        });
        this.newItem="";
      }    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin: 0 10px;
}
.title{
  padding:20px;
}
.content{
  padding:20px;
}
.finished{
  text-decoration:line-through;
}

</style>
