<template>
  <section>
    counter: {{ $store.state.counter.counter}}
    <button @click="$store.commit('counter/countUp')">+1</button>
    <button @click="$store.commit('counter/reset')">reset</button>
  </section>
</template>

<script>
  export default{
    data: function(){
      return {
        title: 'Counter'
      }
    }
  }
</script>