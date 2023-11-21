
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>Va rugam introduceti de la tastaura numere cuprinse intre 100 si 999 despartite prin virgula.</p>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}  
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  margin-bottom: 100px;
  color:rgb(0, 17, 255);
}

</style>
