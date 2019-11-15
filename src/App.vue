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
        stopFlg: false,
      }
    },
    methods:{
      start(){
        while(!this.stopFlg){
          this.showNumber = this.rand(this.startNumber, this.endNumber);
        }
      },
      show(){
        this.stopFlg = true;
        let number = this.randomCount();
        // ここで何かしらの処理
        // let step;
        // for (step = 0; step < 10; step++){
        //   setTimeout(() => {
        //             this.showNumber = this.rand(this.startNumber, this.endNumber);
        //           }
        //           ,1000);
        // }
        this.showNumber = number;
        this.alreadyNumber.unshift(number);
      },
      randomCount() {
        let number = this.rand(this.startNumber, this.endNumber);

        while(this.showNumber <= this.endNumber){
          if (this.bool(number)) {
            break;
          }
          if (this.alreadyNumber.length >= this.endNumber){
            break;
          }
          number = this.rand(this.startNumber,this.endNumber);
        }
        return number;
      },
      rand(min, max){
        return Math.floor(Math.random() * (max - min + 1) + min);
      },
      bool(number){
        return this.alreadyNumber.indexOf(number) < 0;
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
