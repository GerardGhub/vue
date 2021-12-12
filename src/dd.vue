 <template>
  <div id="app">
      <Header />
    <AddTodo v-on:add-todo="addTodo"/>
    <!--img alt="Vue logo" src="./assets/logo.png"  text below is template directive -->
    <todos v-bind:todosy="todosy" v-on:del-todo="deleteTodo"/>
  
<todos/>
  </div>
</template> 

<script>

import todos from './components/todos';
import AddTodo from './components/AddTodo';
import Header from './components/layout/header';
import axios from 'axios';
export default {
  name: 'App',
  components: {
    todos,
    AddTodo,
    Header 
  },
  data(){
    return{
      todosy:[

      /*  {
          id:1,
          title: "Todo One",
          completed: false
        },
                {
          id:2,
          title: "Todo Two",
          completed: false
        },
        {
          id:3,
          title: "Todo Three",
          completed: false
        }
        */
      ]
    }
  }
  ,
  methods:{
    deleteTodo(id)
    {
      
      axios.delete('https://jsonplaceholder.typicode.com/todos/${id}')
      .then(res =>{
        this.todosy = this.todosy.filter(todo => todo.id !== id)
        return res
      })

      .catch(error => {
  return Promise.reject(error);
})
      //this.todosy = this.todosy.filter(todo=> todo.id !== id)
    },
    addTodo(newTodo)
        {
const {title, completed} = newTodo;
axios.post('https://jsonplaceholder.typicode.com/todos',{
  title,
  completed
})
.then(res => this.todosy = [...this.todosy, res.data])
.catch(error => {
  return Promise.reject(error);
})
//this.todosy = [...this.todosy, newTodo]; 
        }
  },
  created(){
axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
.then(res => this.todosy = res.data)
.catch(error => {
  return Promise.reject(error);
})

  }


}
</script>

<style>
#app {
margin: 0;
padding: 0;
box-sizing: border-box;
}
body{
  font-family: Arial, Helvetica, sans-serif;
}
.btn{
  display: inline;
  border: none;
  background: #555;
    color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover{
  background: #666;
  color: #fff;
}
</style>
