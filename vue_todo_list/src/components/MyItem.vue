<template>
    <li>
        <label>
        <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)"/>
        <span v-show="!todo.isEdit">{{todo.title}}</span>
        <input 
        type="text" 
        v-show="todo.isEdit" 
        :value="todo.title" 
        @blur="handleBlur(todo,$event)"
        ref="inputTitle"
        >
        </label>
        <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
        <button 
        class="btn btn-edit" 
        @click="handleEdit(todo)"
        v-show="!todo.isEdit"
        >编辑</button>
    </li>
</template>
<script>
// import pubsub from 'pubsub-js' //pubsub方法导入
export default {
  name: "MyItem",
  //声明接受对象
  props: ["todo"],
  methods: {
    handleCheck(id) {
      this.$bus.$emit("checkTodo", id);
    },
    handleDelete(id) {
      //给父组件函数传id,让父函数删除id对应的数组
      if (confirm("确定删除吗")) {
        this.$bus.$emit("deleteTodo", id); //总线方法
        // pubsub.publish('deleteTodo',id)   //pubsub发布消息方法
      }
    },
    handleEdit(todo) {
      //编辑
      if (Object.prototype.hasOwnProperty.call(todo, "isEdit")) {
        todo.isEdit = true;
      } else {
        //需要考虑空和false问题
        this.$set(todo, "isEdit", true);
      }
      //生命周期updated之后执行
      this.$nextTick(function(){
        this.$refs.inputTitle.focus()
      })
    },
    handleBlur(todo,e) {
      todo.isEdit = false;
      if(!e.target.value.trim()) return alert('输入不能为空')
      this.$bus.$emit("updateTodo", todo.id,e.target.value)
    }
  }
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
li:hover button {
  display: block;
}
</style>
