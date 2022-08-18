<!-- eslint-disable no-unused-vars -->
<!-- eslint-disable vue/no-unused-vars -->

<template>
  <div class="row todo-content">
    <div class="col-md-6">
      <div class="todo-list not-done">
        <h1>TODOS</h1>
        <div class="input-group mb-3">
          <input type="text" class="form-control" placeholder="Enter content" v-model="textContent">
          <div class="input-group-append">
            <button class="btn btn-outline-secondary" type="button" id="button-addon2" @click="addTask()">Add</button>
          </div>
        </div>
        <hr>
        <ul class="list-unstyled" v-for="(todo,index) in todos" :key="todo.id">

          <li class="ui-state-default li-items mt-1">
            <div class="input-group">
              <div class="input-group-prepend">
                <div class="input-group-text">
                  <input type="checkbox" aria-label="Radio button for following text input" :checked="todo.checked" v-model="todo.checked">
                </div>
              </div>
              <input type="text" class="form-control" :class="{'done-task' : todo.completed}" v-model="todo.content">
              <div class="input-group-append remove-icon">
                <span class="input-group-text" @click="delTask(index)">&#10060;</span>
              </div>
            </div>
          </li>

        </ul>
        <hr>
        <div class="todo-footer row">
          <div class="col-md-6">
            <div class="form-check form-check-inline" @click="checkAll(true)">
              &#9989;
              <label class="form-check-label" for="inlineRadio1">Check all</label>
            </div>
            <div class="form-check form-check-inline" @click="checkAll(false)">
              &#10062;
              <label class="form-check-label" for="inlineRadio2">UnCheck all</label>
            </div>
          </div>
          <div class="col-md-6 save-all">
            <div class="form-check form-check-inline save-all">
              <button @click="doneAll()" type="button" class="btn btn-success btn-sm">DONE ALL &#10004;</button>
            </div>
            <div class="form-check form-check-inline save-all">
              <button @click="delAll" type="button" class="btn btn-dark btn-sm">DEL ALL &#10006;</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import axios from 'axios'
export default {
// eslint-disable-next-line vue/multi-word-component-names
name:'Todos',
data() {
  return{
    todos:[
      {
        id:1,
        content:'nội dung 1',
        checked:false,
        completed:false
      },
      {
        id:2,
        content:'nội dung 2',
        checked:true,
        completed:true
      }
    ],
    textContent:'',
    code:2,
  }
},
// created(){
//   axios.get('https://gorest.co.in/public/v2/todos')
//   .then(response=> {
//     this.todos = response.data
//   })
// },
methods:{
  addTask(){
    if(this.textContent.trim().length===0){
      return alert('vui lòng nhập')
    } 
    this.code++
    this.todos.push(
      {
        id:this.code,
        content:this.textContent,
        checked:false,
        completed:false
      }
    )
    this.textContent=''
    
  },
  delTask: function(index){
    if(confirm('Bạn có muốn xoá không?')){
      this.todos.splice(index,1)
    }
  },
  checkAll:function(flag){
    this.todos.forEach(todo => {
      todo.checked=flag;
    })
  },
  doneAll:function(){
  if(confirm('Bạn có muốn hoàn thành tất cả nhiệm vụ không?')){
    this.todos.filter(function(item){
      if(item.checked){
        item.completed=true
      }
    })
  }
  this.checkAll(false)
},
delAll:function(){
  if(confirm('Bạn có muốn xoá không?')){
    this.todos= this.todos.filter(function(item){
     return !item.checked
    })
  }
}
}
}
</script>

<style scoped>
  .todo-content {
    display: flex;
    justify-content: center;
  }

  .todo-list h1 {
    margin-top: 20px;
    padding-bottom: 20px;
    text-align: center;
    font-weight: bold;
  }

  .todo-footer {
    background-color: #d2e8ca;
    padding: 10px 20px 15px;
  }

  #done-items li {
    padding: 10px 0;
    border-bottom: 1px solid #ddd;
    text-decoration: line-through;
  }

  .done-task {
    text-decoration: line-through;
    color: orange;
  }

  .form-check-inline {
    cursor: pointer;
  }

  .remove-icon span {
    cursor: pointer;
  }

  .save-all {
    float: right;
  }
</style>