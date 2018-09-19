<template lang="html">
  <div class="">

  </div>
</template>

<script>
export default {
  data(){
    return{

    }
  },
  methods:{
    A(){
      var Web3 = require("web3");
      var Tx = require('ethereumjs-tx');
      // if(typeof web3 !=='undefined'){
      //   web3=new Web3(web3.currentProvider);
      // }else{
      //
      // }
      var web3=new Web3(new Web3.providers.HttpProvider('https://mainnet.infura.io/v3/3e54236f821f47f08f7294fc2a54e974'));
      console.log(web3)
      var balanceWei=web3.eth.getBalance('0x8896718Ce4dAF41ebA110c63c2A560b3C70ceEb8');
      var balanceW=balanceWei.toString();
      var balance=web3.utils.fromWei(balanceW,'ether');
      console.log(balance)
    }
  },
  mounted(){
    // this.A()
  }
}
</script>

<style lang="css">
</style>
