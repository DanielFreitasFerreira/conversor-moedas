<template>
  <div class="conversor">
    <h2>{{moedaA}} To {{moedaB}}</h2>
    <input type="text" v-model="moedaA_value" v-bind:placeholder="moedaA">
    <input type="button" value="Converter" v-on:click="converter">
    <h2>{{moedaB_value}}</h2>
  </div>
</template>


<script>
  export default {
    name: "Conversor",
    props: ["moedaA", "moedaB"],
    data() {
      return {
        moedaA_value: "",
        moedaB_value: 0
      };
    },
    methods: {
      converter() {
        let de_para = this.moedaA + '_' + this.moedaB;
        let url = 'https://free.currencyconverterapi.com/api/v6/convert?q=' + de_para + '&compact=y&apiKey=9efaf120b22fde4b9a53';
        fetch(url)
          .then(res => {
            return res.json()
          })
          .then(json => {
            let cotacao = json[de_para].val;
            this.moedaB_value = (parseFloat(this.moedaA_value) * cotacao).toFixed(2)
          })
      }
    }
  };
</script>


<style scoped >
  .conversor {
    padding: 20px;
    max-width: 300px;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  }
  .conversor input {
    padding: 10px;
  }
  .conversor input + input {
    background-color: #51b983;
    border: 0;
    padding: 10px;
  }
</style>