<template>
  <div class="hello">
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  methods:{
    test(){
      var Web3 =require('web3');
      var Tx=require('ethereumjs-tx');

      // Erc20合约地址
      var contractAddress='0xFf0677aA319585FEcD5b06A0bae4D918422CE0e5';

      // 创建Web3对象
      var web3=new Web3();

      //连接到mainnet线上节点
      console.log(web3)
      var web3=new Web3(new Web3.providers.HttpProvider('https://mainnet.infura.io/v3/3e54236f821f47f08f7294fc2a54e974'));

      //获取已部署的合约对象
      var abi=
      [{"constant":true,"inputs":[],"name":"name","outputs":[{"name":"","type":"string"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_spender","type":"address"},{"name":"_value","type":"uint256"}],"name":"approve","outputs":[{"name":"success","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"totalSupply","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"name":"getData","constant":false,"inputs":[{"name":"_from","type":"address"},{"name":"_to","type":"address"},{"name":"_value","type":"uint256"}],"name":"transferFrom","outputs":[{"name":"success","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"decimals","outputs":[{"name":"","type":"uint8"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"version","outputs":[{"name":"","type":"string"}],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_owner","type":"address"}],"name":"balanceOf","outputs":[{"name":"balance","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"symbol","outputs":[{"name":"","type":"string"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_to","type":"address"},{"name":"_value","type":"uint256"}],"name":"transfer","outputs":[{"name":"success","type":"bool"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_spender","type":"address"},{"name":"_value","type":"uint256"},{"name":"_extraData","type":"bytes"}],"name":"approveAndCall","outputs":[{"name":"success","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_owner","type":"address"},{"name":"_spender","type":"address"}],"name":"allowance","outputs":[{"name":"remaining","type":"uint256"}],"payable":false,"type":"function"},{"inputs":[],"payable":false,"type":"constructor"},{"payable":false,"type":"fallback"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_from","type":"address"},{"indexed":true,"name":"_to","type":"address"},{"indexed":false,"name":"_value","type":"uint256"}],"name":"Transfer","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_owner","type":"address"},{"indexed":true,"name":"_spender","type":"address"},{"indexed":false,"name":"_value","type":"uint256"}],"name":"Approval","type":"event"}];
      var coinContract=web3.eth.contract(abi).at(contractAddress);

      console.log(coinContract)

      var fromAddress='0xCF12aED774CA064F28a70012f8BEDE6B6E323e16';
      var toAddress='0x8896718Ce4dAF41ebA110c63c2A560b3C70ceEb8';
      var count=web3.eth.getTransactionCount(fromAddress);
      var gasPrice=web3.eth.gasPrice;
      var gasLimit=90000;

      //余额查询
      var tokenBalance=coinContract.balanceOf(fromAddress);
      console.log(tokenBalance)
      console.log(tokenBalance.toNumber())
      // var a=tokenBalance.toNumber();
      // console.log(a.ceil())
      // 转账
      console.log(coinContract.transfer)
      // var data=coinContract.transfer(toAddress,100000000000,{from:fromAddress});
      // console.log(data)
      var rawTransaction={
        'from':fromAddress,
        'nonce':web3.toHex(count),
        'gasPrice':web3.toHex(gasPrice),
        'gasLimit':web3.toHex(gasLimit),
        'value':'0.002',
        'to':toAddress
      };
      console.log(rawTransaction)

      //读取私钥，截取掉‘0x’
      var privKey=new Buffer.from('33d3fcb04974671099b548b9bf684b23425016574a25aa507cb9c0ca677a3a97','hex');
      var tx=new Tx(rawTransaction);
      console.log(tx)

      // //签名交易信息
      tx.sign(privKey);
      var serializedTx=tx.serialize();
      console.log(serializedTx)

      //发送交易
      web3.eth.sendRawTransaction('0x'+serializedTx.toString('hex'),function(err,hash){
        if(!err){
          console.log(hash)
        }else{
          console.log(err)
        }
      })
    }
  },
  mounted(){
    this.test()
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
