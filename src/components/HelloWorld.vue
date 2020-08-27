<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>NA PLUSIE: {{onPlus}}   NA MINUSIE {{onMinus}}</p>
    <p>BILANS: {{suma}}</p>
    <div v-for="item in records" :key="item.id" v-bind:class="[item['TYP'] == 'Transakcja Kupna' ? green : item['TYP'] == 'Koszty Utrzymania Pozycji' ? yellow : 
    item['TYP'] == 'Zamknięcie Transakcji' ? red : item['TYP'] == 'Transakcja Sprzedaży' ? blue : white, 'box']">
      <p>DATA: {{item['DATA/CZAS']}}</p>
      <p>TYP: {{item['TYP']}}</p>
      <p>INSTRUMENT: {{item['INSTRUMENT']}}</p>
      <p>CENA: {{item['CENA']}}</p>
      <p>WARTOŚĆ POZYCJI: {{item['WARTOŚĆ POZYCJI (PLN)']}}</p>
      <p>KOSZTY UTRZYMANIA POZYCJI: {{item['KOSZTY UTRZYMANIA POZYCJI - SUMA (PLN)']}}</p>
      <p>ZAKSIĘGOWANA KWOTA: {{item['ZAKSIĘGOWANA KWOTA (PLN)']}}</p>
      <p>KURS WYMIANY: {{item['KURS WYMIANY']}}</p>
    </div>
  </div>
</template>

<script>
import Historia from '../Historia.json'
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  created: function() {
    for(let item of Historia){
      this.records.push(item)
      this.testItem = item;
      if(parseInt(item['ZAKSIĘGOWANA KWOTA (PLN)'], 10) > 0){
        this.onPlus += parseInt(item['ZAKSIĘGOWANA KWOTA (PLN)'], 10);
      } else if(parseInt(item['ZAKSIĘGOWANA KWOTA (PLN)'], 10) < 0){
        this.onMinus -= parseInt(item['ZAKSIĘGOWANA KWOTA (PLN)'], 10);
      }
    }
    for(let property in this.testItem){
      console.log(property);
    }
    console.log(this.testItem);
    this.suma = this.onPlus - this.onMinus;
    
  },
  methods: {
    showRecords: function(){
      for(let item of Historia){
        console.log(item);
      }
    }
  },
  data: function(){
    return{
      records: [],
      counter: 1,
      testItem: '',
      green: 'green',
      white: 'white',
      yellow: 'yellow',
      red: 'red',
      blue: 'blue',
      onPlus: 0,
      onMinus: 0,
      suma: 0,
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
.box {
  border: solid;
  border-width: 2px;
  margin: 2px;
}
.green {
  background-color: lightgreen;
}
.yellow {
  background-color: yellow;
}
.red {
  background-color: red;
}
.blue {
  background-color: lightblue;
}
</style>
