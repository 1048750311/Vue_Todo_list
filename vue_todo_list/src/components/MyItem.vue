<template>
    <li>
        <label>
        <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)"/>
        <span>{{todo.title}}</span>
        </label>
        <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
    </li>
</template>
<script>
import pubsub from 'pubsub-js'
export default {
  name: "MyItem",
  //声明接受对象
  props:['todo'],
  methods: {
      handleCheck(id){
          this.$bus.$emit('checkTodo',id)
      },
      handleDelete(id){//给父组件函数传id,让父函数删除id对应的数组
          if(confirm('确定删除吗')){
            //  this.$bus.$emit('deleteTodo',id) //总线方法
            pubsub.publish('deleteTodo',id)   //pubsub发布消息方法
            
          } 
      }
  },
};
</script>
<style lang="css" scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}
li:hover {
  background-color: #ddd;
}
li:hover button{
  display: block;
}
</style>
