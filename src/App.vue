<template class="temp">
  <div id="app" style="text-align: center">
    <span class="title" v-if="!spinButton">{{ showNumber }}</span>
    <span class="title" v-else>{{ rouletteNumber }}</span><br>
    <button @click="start" v-if="!spinButton">スタート</button>
    <button @click="show" v-else>ストップ</button>
    <p class="already">{{ alreadyNumber }}</p>
  </div>
</template>

<script>
  import drum from './assets/drum.mp3';
  import cymbal from './assets/cymbal.mp3';

  export default {
    name: 'app',
    data() {
      return {
        alreadyNumber: [],
        endNumber: 99,
        startNumber:0,
        showNumber: "",
        rouletteNumber: "",
        spinButton: false,
        music: {},
      }
    },
    mounted(){
      setInterval(function() {
        this.rouletteNumber = this.getNumber();
      }.bind(this) ,100);
    },
    methods:{
      start(){
        this.spinButton = true;
        this.music = new Audio(drum);
        this.music.play();
      },
      show(){
        this.music.pause();
        this.spinButton = false;
        const audio = new Audio(cymbal);
        audio.play();

        let number = this.randomCount();
        this.showNumber = number;
        this.alreadyNumber.unshift(number);
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
    },
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
