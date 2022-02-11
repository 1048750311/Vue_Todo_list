<template>
    <div class="todo-header">
        <input type="text" placeholder="请输入你的任务名称，按回车键确认"  v-model="title"  @keyup.enter="add"/>
    </div>
</template>
<script>
import {nanoid} from 'nanoid'
export default {
  name: "MyHeader",
  data() {
      return {
          title:''
      }
  },
  methods: {
    add() {//子组件定义一个添加函数，调用父组件传递过来的添加函数
        //检查输入数据
        if(!this.title.trim()) return alert('输入不为空')
        //将用户的输入包装成一个todo对象
        const todoobj = {id:nanoid(), title:this.title, done:false}
        //通知App主见去添加一个todo
        this.$emit('addTodo', todoobj)
        this.title=''
        
        
    }
  }
};
</script>
<style lang="css" scoped>
/*header*/
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(82, 168, 236, 0.6);
}
</style>
