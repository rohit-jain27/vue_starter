<template>
  <div id="app">
    <button v-on:click="showPollDetails=true">New Poll</button>
    <div v-if="showPollDetails">
      <div>Poll Name</div>
      <input v-model="pollName" placeholder="Poll name">

      <div
        v-for="(item, index) in pollOptions"
        v-bind:key="index">
        <div>Question {{index+1}}</div>
        <input v-model="item.question" placeholder="Enter poll option">
      </div>

      <button v-on:click="pollOptions.push({question:''})">New Option</button>
    </div>

    <button v-on:click="startGame()">Start Game</button>
    <div v-on:click="calculateCircle(); decrementScore();" id="box">
      <div v-on:click="incrementScore()" v-bind:style="{ position: 'absolute', top: top + 'px', left: left + 'px', width: '10px', height: '10px', backgroundColor: 'red' }"/>
      <!-- <div id="circle"/> -->
      <!-- <div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div> -->

    </div>
    <div>{{score}}</div>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'app',
  data: function () {
    return {
      top: 100,
      left: 100,
      score: 0,
      showPollDetails: false,
      pollName: '',
      pollOptions: [
        {
          question: '',
        },
        {
          question: '',
        }
      ]
    }
  },
  methods: {
    say: function (message) {
      alert(message)
    },
    calculateCircle: function() {
      this.top = Math.min(Math.random()*400, 400);
      this.left = Math.min(Math.random()*400, 400);
    },
    startGame: function() {
      this.calculateCircle();
      setTimeout(() => {
        this.startGame();
        this.score -= 100;
      }, 1500)
    },
    incrementScore: function() {
      this.score += 200;
    },
    decrementScore: function() {
      this.score -= 100;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#box {
  height: 400px;
  width: 400px;
  border: 1px solid black;
  position: relative;
}
#circle {
  position: absolute;
  top: 10px;
  left: 10px;
  background-color: red;
  width: 10px;
  height: 10px;

}
</style>
