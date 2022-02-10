<template>
    <div class="todo-footer">
        <label>
        <input type="checkbox"/>
        </label>
        <span>
        <span>已完成{{doneTotal}}</span> / 全部{{todos.length}}
        </span>
        <button class="btn btn-danger">清除已完成任务</button>
    </div>
</template>
<script>
export default {
    computed:{
      doneTotal(){
        //第一种foreach方法
        // let i = 0
        // this.todos.forEach(todo => {
        //   if(todo.done) i++ 
        // });
        // return i
        
        //第二种filter方法
        // return (this.todos.filter(todo => todo.done === true)).length

        //第三种reduce方法reduce(pre,current)
        // const x = this.todos.reduce((pre,current)=>{
        //   return pre + (current.done? 1 : 0)
        // },0)
        //第三中简化
        return this.todos.reduce((pre,current)=> pre + (current.done? 1 : 0),0)
      }
    },
    name:'MyFooter',
    props:['todos']
}
</script>
<style lang="css" scoped>
  /*footer*/
  .todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
  }

  .todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
  }

  .todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
  }

  .todo-footer button {
    float: right;
    margin-top: 5px;
  }

</style>
