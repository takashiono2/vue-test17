<template>
  <seciton class="countainer">
    <div>
      <Counter />
      <hr>
      <Counter />
      <hr>
      <Counter />
      <hr>
    </div>
  </seciton>
</template>

<script>
import Counter from '~/components/Counter.vue'

export default {
  components: {
    Counter
  }
}
</script>
