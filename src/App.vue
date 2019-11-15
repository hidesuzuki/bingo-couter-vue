<template class="temp">
  <div id="app" style="text-align: center">
    <span class="title">{{ showNumber }}</span><br>
    <button @click="start">スタート</button>
    <button @click="show">押して</button>
    <p class="already">{{ alreadyNumber }}</p>
  </div>
</template>

<script>

  export default {
    name: 'app',
    data() {
      return {
        alreadyNumber: [],
        endNumber: 99,
        startNumber:0,
        showNumber: "",
        spinButton: false,
      }
    },
    mounted() {
      setInterval(function() {
        //this.showNumber = this.getNumber();
      },100);
      // this.showNumber = setInterval(function() {
      //   // ルーレット
      //   this.rand(this.startNumber, this.endNumber);
      // }, 1000);
    },
    methods:{
      start(){
        this.spinButton = true;
        // this.showNumber = setInterval(function() {
        //   // ルーレット
        //   return 20;
        // }, 1000);
        this.showNumber = this.getNumber();
      },
      show(){
        this.spinButton = false;
        clearInterval(this.showNumber);

        let number = this.randomCount();
        this.showNumber = number;
        this.alreadyNumber.unshift(number);
      },
      loopCount(){
        this.sleep(10).then(() => {
          this.showNumber = this.getNumber();
          return this.sleep(10);
        }).then(() => {
          this.showNumber = this.getNumber();
        });
      },
      randomCount() {
        let number = this.getNumber();

        while(this.showNumber <= this.endNumber){
          if (this.bool(number)) {
            break;
          }
          if (this.alreadyNumber.length >= this.endNumber){
            break;
          }
          number = this.getNumber();
        }
        return number;
      },
      getNumber() {
        return this.rand(this.startNumber,this.endNumber);
      },
      rand(min, max){
        return Math.floor(Math.random() * (max - min + 1) + min);
      },
      bool(number){
        return this.alreadyNumber.indexOf(number) < 0;
      },
      sleep(time){
        return new Promise((resolve) => {
          setTimeout(() => {
            resolve();
          }, time);
        });
      }
    }
  }
</script>

<style>
  .title{
    font-size: 800px;
    color: white;
  }
  .already{
    color: white;
    font-size: 50px;
  }
  #app{
    background-color: crimson;
  }
</style>
