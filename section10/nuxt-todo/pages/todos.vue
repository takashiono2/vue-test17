<template>
  <div>
    <!-- {{ todos }} -->
    <ul>
      <li v-for="todo in todos" :key="todo.id">
        <!-- {{ todo }} -->
        <span v-if="todo.created">
          <input type="checkbox"
            :checked="todo.done"
            @change="toggle(todo)"
          >
          <span :class="{done: todo.done}">
            {{ todo.name }},{{ todo.created.toDate() | dataFilter }}
          </span>
          <button @click="remove(todo.id)">X</button>
        </span>
      </li>
    </ul>
    <div class="form">
      <form @submit.prevent="add"><!--formのAddで送信したら、addが機能する。意図しない画面遷移を避ける-->
        <input v-model="name"><!--nameで紐づける-->
        <button>Add</button>  
      </form>
    </div>
  </div>
</template>

<script>
  import moment from 'moment'
  export default{
    data(){
      return {
        name: '',//inputとnameで紐づく
        done: false
      } 
    },
    created(){
      this.$store.dispatch('todos/init')//todosのactionsのinitで実行、
    },
    methods:{
      add(){
        this.$store.dispatch('todos/add',this.name)//todosのactionsのinitで実行、引数は、this.name
        this.name =""//フォームを初期化(空にしておく)
      },
      remove(id){
        this.$store.dispatch('todos/remove',id)
      },
      toggle(todo){
        this.$store.dispatch('todos/toggle',todo)
      },
    },
    computed: {
      todos(){
        return this.$store.state.todos.todos
      }
    },
    filters: {
      dataFilter: function(date){
        return moment(date).format('YYYY/MM/DD HH:mm:ss')
      }
    }
  }
</script>

<style>
  li > span.done{
    text-decoration: line-through;
  }
</style>