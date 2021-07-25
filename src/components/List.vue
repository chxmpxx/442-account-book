<template>
  <div class="line">
    <img src="../assets/02.png">
    <br><br>
    <h1>List</h1>
    <br>

    <div class="list">
      <table>
        <thead>
          <tr>
            <th>&nbsp;&nbsp;Date</th>
            <th>Category</th>
            <th>Memo</th>
            <th>Amount</th>
            <th>Total</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(list, index) in inputs" :key="index"> 
            <td>
              {{ list.date }}
            </td>
            <td>
              {{ list.category }}
            </td>
            <td>
              {{ list.memo }}
            </td>
            <td>
              {{ list.amount }}
            </td>
            <td>
              {{ list.total }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <br><br>
  </div>
</template>

<script>
import InputStore from '@/store/InputStore.js'
export default {
  data(){
    return{
      inputs:[],
      form: {
        date: '',
        amount: '',
        category: '',
        memo: ''
      },
      total: ''
    }
  },
  created(){
    this.fetchInput()
  },

  methods:{
    fetchInput(){
      InputStore.dispatch('fetchData')
      this.inputs = InputStore.getters.inputs
    },
  }
}
</script>

<style lang="scss" scoped>
img{
display: block;
  margin-left: auto;
  margin-right: auto;
  width: 100%;
}
h1{
  color: #4B4B4B;
  font-size: 36px;
  background-color: #FFE0D8;
  border-style: dashed;
  border-width: 1.5px;
  border-radius: 15px;
  margin: 0em 30em 0em 2em;
  padding: 0.1em;
}
.list{
  color: #4B4B4B;
  background-color: #FFE0D8;
  border-style: dashed;
  border-width: 1.5px;
  border-radius: 15px;
  margin: 0em 4.5em 0em 4.5em;
  padding: 0.5em 0 0.5em 0;
}
th{
  font-size: 24px;
  padding: 0.5em 3em 0.5em 3em;
}
td{
  font-size: 20px;
}
</style>