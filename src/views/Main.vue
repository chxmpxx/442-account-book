<template>
  <div class="main">
    <div class="head">
      <br><br><br><br><h1>Account Book</h1>
    </div>
    <br><br>

    <Input/>
    <List/>
    <Graph/>
  </div>
</template>

<script>
// @ is an alias to /src
import Input from '@/components/Input.vue'
import List from '@/components/List.vue'
import Graph from '@/components/Graph.vue'

export default {
  name: 'Main',
  components: {
    Input,
    List,
    Graph
  }
}
</script>

<style>
body{
margin: 0
}
.main{
  background-color: #FFF6E5;
}
.head{
  background-image: url(../assets/01.png);
  background-size: cover;
  background-position: center;
}
h1{
  color: #4B4B4B;
  font-size: 60px;
}
</style>