<template>
  <div class="input">
    <br><br>
    <h1>Input</h1>
    <br>

    <div class="creat">
      <div>
        <label for="date">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Date</label>
        <input type="date" v-model="form.date">
    
        <label for="amount">&nbsp;Amount</label>
        <input type="text" v-model="form.amount">
      </div>
      <div>
        <label for="category">&nbsp;&nbsp;&nbsp;Category</label>
        <input type="text" v-model="form.category">
    
        <label for="memo">&nbsp;&nbsp;&nbsp;Memo</label>
        <input type="text" v-model="form.memo">
      </div>
      <div>
        <button id="income-1" class='income' @click="income(1)">Income</button>
        <button id="expense-2" @click="expense(-1)">Expense</button>
        <button class='complete' @click="addInput">Complete</button>
      </div>
    </div>
    <br><br>
  </div>
</template>

<script>
import InputStore from '@/store/InputStore.js'
export default {
  data(){
    return{
      type: 1,
      form: {
        date: '',
        amount: '',
        category: '',
        memo: ''
      },
      total: 850,
      inc: 3200,
      exp: -2350
    }
  },

  methods: {
    income(type){
      this.type = type;
      console.log(type);

      document.getElementById("income-1").style.backgroundColor = "#F2939B";
      document.getElementById("expense-2").style.backgroundColor = "#FFE0D8";
    },
    expense(type){
      this.type = type;
      console.log(type);

      document.getElementById("expense-2").style.backgroundColor = "#F2939B";
      document.getElementById("income-1").style.backgroundColor = "#FFE0D8";
    },
    clearForm() {
      this.form = {
        date: '',
        amount: '',
        category: '',
        memo: ''
      }
    },
    addInput() {
      this.form.amount = Number(this.form.amount)
      if(this.type === -1){
        this.form.amount = this.form.amount*-1
        this.exp = this.exp+this.form.amount
      }else{
        this.inc = this.inc+this.form.amount
      }
      this.total = this.total+this.form.amount
      let payload = {
        date: this.form.date,
        amount: this.form.amount,
        category: this.form.category,
        memo: this.form.memo,
        total: this.total,
        inc : this.inc,
        exp : this.exp
      }
      console.log(payload)
      console.log(this.exp,this.inc)
      InputStore.dispatch("addInput", payload)
      this.clearForm()
    },
  },
}
</script>

<style lang="scss" scoped>
.input{
  background-color: #FFE0D8;
}
h1{
  color: #4B4B4B;
  font-size: 36px;
  background-color: #FFF6E5;
  border-style: dashed;
  border-width: 1.5px;
  border-radius: 15px;
  margin: 0em 30em 0em 2em;
  padding: 0.1em;
}
.creat{
  color: #4B4B4B;
  font-size: 24px;
  background-color: #FFF6E5;
  border-style: dashed;
  border-width: 1.5px;
  border-radius: 15px;
  margin: 0em 3em 0em 3em;
  padding: 0.5em 0 0.5em 0;
}
input{
  color: #4B4B4B;
  font-size: 24px;
  margin: 0.5em 1.4em 0.4em 0.4em;
}
button{
  color: #4B4B4B;
  font-size: 18px;
  background-color: #FFE0D8;
  border-width: 1px;
  width: 5em;
  height: 2em;
  margin: 0.5em 1em 0.5em 0em;
}
button:hover{
  box-shadow: 1px 1px #F2939B, 5px 5px #FEF7C1;
}
.income{
  margin-left: 11.5em;
  background-color : #F2939B;
}
.complete{
  margin-left: 17.5em;
}
.complete:active{
  background-color: #F2939B;
}
input{
  width: 12em;
}

</style>