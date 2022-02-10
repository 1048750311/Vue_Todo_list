<template>

  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader :addTodo="addTodo"/>
        <!-- 下面通过传函数方式实现子组件向父组件通信 -->
        <MyList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"/>
        <MyFooter/>
      </div>
    </div>
  </div>

</template>

<script>
 import MyHeader from './components/MyHeader.vue'
 import MyList from './components/MyList.vue'
 import MyFooter from './components/MyFooter.vue'

export default {
  name: 'App',
  components:{MyHeader,MyList,MyFooter},
   data() {
    return {
      todos:[
        {id:'001', title:'堡垒之夜', done:true},
        {id:'002', title:'英雄联盟', done:false},
        {id:'003', title:'星际争霸2', done:true},
      ]
    }
  },
  methods: {
    addTodo(todoobj){//添加一个todo
      //添加进数组，通过传递函数，让子主见向夫组件提交数据与另一个子组件通信
      this.todos.unshift(todoobj)
      
    },
    checkTodo(id){//勾选是否完成
      this.todos.forEach((todo) => {
        if(todo.id === id) todo.done = !todo.done
      });
    },
    deleteTodo(id){//接受子组件id,删除一个todo
      this.todos= this.todos.filter( todo => todo.id !== id)
    }
  }
}
</script>

<style>

  /*base*/
  body {
    background: #fff;
  }

  .btn {
    display: inline-block;
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
  }

  .btn-danger {
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
  }

  .btn-danger:hover {
    color: #fff;
    background-color: #bd362f;
  }

  .btn:focus {
    outline: none;
  }

  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }

  




</style>
