<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Vue Js Design Model of the Guia Código</h2>
    <ul>



      <li>
        <a
          href="https://guiacodigo.com"
          target="_blank"
        >
          Guia Código
        </a>
      </li>
      <li>
        <a
          href="https://twitter.com/guiacodigo"
          target="_blank"
        >
          Twitter
        </a>
      </li>
    </ul>

  </div>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      msg: 'Have a coffee with Vue JS!'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
