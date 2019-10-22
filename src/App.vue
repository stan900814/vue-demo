<template>
  <div id="app">
    <h2>井字棋游戏</h2>
    <div class="chess">
      <div class="row">
      <Box @click="onClickBox(0,$event)" :n="n"></Box>
      <Box @click="onClickBox(1,$event)" :n="n"></Box>
      <Box @click="onClickBox(2,$event)" :n="n"></Box>
    </div>
    <div class="row">
      <Box @click="onClickBox(3,$event)" :n="n"></Box>
      <Box @click="onClickBox(4,$event)" :n="n"></Box>
      <Box @click="onClickBox(5,$event)" :n="n"></Box>
    </div>
    <div class="row">
      <Box @click="onClickBox(6,$event)" :n="n"></Box>
      <Box @click="onClickBox(7,$event)" :n="n"></Box>
      <Box @click="onClickBox(8,$event)" :n="n"></Box>
    </div>
    <h2 class="result">
      {{result}}
    </h2>
</div>
  </div>
</template>

<script>
import Box from "./components/Box";

export default {
  name: "app",
  data() {
    return {
      n: 0,
      map: [[null, null], [null, null], [null, null]],
      result: ""
    };
  },
  components: {
    Box
  },
  methods: {
    onClickBox(i, text) {
      this.map[Math.floor(i / 3)][i % 3] = text;
      this.n += 1;
      this.judge();
      if (this.result !== "") {
        return;
      }
    },
    judge() {
      for (let i = 0; i < 2; i++) {
        if (
          this.map[i][0] !== null &&
          this.map[i][0] === this.map[i][1] &&
          this.map[i][1] === this.map[i][2]
        ) {
          this.result = `游戏结束：${this.map[i][0]}方获得胜利！`;
        }
      }
      for (let j = 0; j < 2; j++) {
        if (
          this.map[0][j] !== null &&
          this.map[0][j] === this.map[1][j] &&
          this.map[1][j] === this.map[2][j]
        ) {
          this.result = `游戏结束：${this.map[0][j]}方获得胜利！`;
        }
      }
      if (
        this.map[0][2] !== null &&
        this.map[0][2] === this.map[1][1] &&
        this.map[1][1] === this.map[2][0]
      ) {
        this.result = `游戏结束：${this.map[0][2]}方获得胜利！`;
      }
      if (
        this.map[0][0] !== null &&
        this.map[0][0] === this.map[1][1] &&
        this.map[1][1] === this.map[2][2]
      ) {
        this.result = `游戏结束：${this.map[0][0]}方获得胜利！`;
      }
    }
  }
};
</script>

<style>
#app {
  display: flex;
  text-align: center;
  align-items: center;
  flex-direction: column;
}
.row {
  display: flex;
}
.result {
  color: red;
}
</style>
