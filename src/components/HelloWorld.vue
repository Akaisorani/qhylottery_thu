<template>
  <div>
    <img class="logo" src="@/assets/act_logo.png"/>
    <div class="main">
      <div class="result">
        <div class="result-number">
          <div class="result-number-item" v-for="(item, index) in result" :key="index">{{ item }}</div>
        </div>
        <div class="btn shadow" v-if="!working" @click="startRandom">抽 奖</div>
        <div class="btn shadow" v-else @click="stopRandom">停</div>
      </div>
      <div class="gender">
        <img v-if="male" src="@/assets/male.png"/>
        <img v-else src="@/assets/female.png"/>
      </div>
    </div>
  </div>
</template>

<script>
let task = null;

export default {
  name: 'HelloWorld',
  data() {
    return {
      working: false,
      male: true,
      result: '000'
    }
  },
  mounted() {
  },
  methods: {
    startRandom() {
      this.$data.working = true
      task = setInterval(() => {
        this.generateLottery()
      }, 20)
    },
    stopRandom() {
      this.$data.working = false
      clearInterval(task)
    },
    formatNumber(n) {
      let result = n.toString()
      let length = result.length
      for (let i = length; i < 3; i++) {
        result = '0' + result
      }
      return result
    },
    generateLottery() {
      this.$data.result = this.formatNumber(Math.floor(Math.random() * 100 + 1))
      this.$data.male = Math.random() > 0.5
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.logo {
  position: absolute;
  width: 25vw;
  right: 0;
  bottom: 0;
}

.main {
  position: absolute;
  display: flex;
  flex-direction: row;
  left: 5vw;
  top: 20vh;
}

.result {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.result-number {
  display: flex;
  flex-direction: row;
}

.result-number-item {
  font-size: 15vw;
  margin: 0 2vw;
  padding: 0 2vw;
  border: #2c3e50 10px solid;
  border-radius: 10px;
  color: #7924cb;
  height: 35vh;
  line-height: 35vh;
  background-color: white;
  font-weight: bold;
}

.gender {
  margin-left: 3vw;
}

.gender img {
  height: 25vh;
  margin-top: 5vh;
}

.btn {
  text-align: center;
  margin-top: 8vh;
  font-size: 3vw;
  width: 15vw;
  height: 6vw;
  line-height: 6vw;
  color: rgb(203, 32, 32);
  background: linear-gradient(rgb(251, 220, 15), rgb(255, 166, 3));
  border-radius: 1vw;
  font-weight: bold;
}

.shadow {
  position: relative;
  max-width: 20vw;
  box-shadow: 0px 1px 4px rgba(255, 166, 3, 0.3),
  0px 0px 20px rgba(255, 166, 3, 0.1) inset;
}

.shadow::before,
.shadow::after {
  content: "";
  position: absolute;
  z-index: -1;
}

.shadow::before,
.shadow::after {
  content: "";
  position: absolute;
  z-index: -1;
  bottom: 15px;
  left: 10px;
  width: 50%;
  height: 20%;
}

.shadow::before,
.shadow::after {
  content: "";
  position: absolute;
  z-index: -1;
  bottom: 15px;
  left: 10px;
  width: 50%;
  height: 20%;
  box-shadow: 0 15px 10px rgba(0, 0, 0, 0.7);
  transform: rotate(-3deg);
}

.shadow::after {
  right: 10px;
  left: auto;
  transform: rotate(3deg);
}
</style>
