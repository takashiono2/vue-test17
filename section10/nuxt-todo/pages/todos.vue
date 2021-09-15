<template>
  <div>
    <!-- {{ todos }} -->
    <ul>
      <li v-for="todo in todos" :key="todo.id">
        <!-- {{ todo }} -->
        <span v-if="todo.created">
          <input type="checkbox" :checked="todo.done" @change="toggle(todo)"><!--inputをcheckbox型でチェックが入ったら、変更のタイミングで、toggle(todo)関数で判定 -->
          <span :class="{done: todo.done}">
          <!--spanクラスと紐付けて、tureなら横線を入れる -->
            {{ todo.name }},{{ todo.created.toDate()| dataFilter }}<!--filter関数を使う-->
          </span>
          <button @click="remove(todo.id)">X</button>
          {{ todo.id }}
        </span>
      </li>
    </ul>
    <div class="form">
      <form @submit.prevent="add">
        <input v-model="name">
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
        name: '',
        done: false
      } 
    },
    created(){
      this.$store.dispatch('todos/init')
    },
    methods:{
      add(){
        this.$store.dispatch('todos/add',this.name)
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
        // return this.$store.state.todos.todos
        return this.$store.getters['todos/orderdTodos']
      }
    },
    filters: {
      dataFilter(date){
        return moment(date).format('YYYY/MM/DD HH:mm:ss')
      }//dataFilterという関数で、'YYYY/MM/DD HH:mm:ss'形式でフォーマット
    }
  }
  
</script>

<style>
li > span > span.done{
  text-decoration: line-through;
}/*liのspanタグで横線*/
</style>