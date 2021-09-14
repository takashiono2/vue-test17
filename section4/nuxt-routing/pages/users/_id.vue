<template>
  <section>
    <h1>{{message}}</h1>
    <p>id: {{ this.$route.params.id}}</p>
  </section>
</template>

<script>
export default {
  data(){
    return { message:'/user/_id.vueを表示中' }
  },
  validate({params}){
    return /^\d+$/.test(params.id)//testの()の中身が数値の場合はtrue,数値でない場合はfalseを返す
  }
}

</script>

<style>

</style>