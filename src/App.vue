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
      <h2 class="result">{{result}}</h2>
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
      map: Array(9).fill(null),
      result: ""
    };
  },
  components: {
    Box
  },
  methods: {
    onClickBox(i, text) {
      this.map[i] = text;
      this.n += 1;
      this.judge(this.map);
      if (this.result !== "") {
        return;
      }
    },
    judge(arr) {
      const lines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
      ];
      for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i];
        if (arr[a] && arr[a] === arr[b] && arr[a] === arr[c]) {
          this.result = `Winner is：${arr[a]}`;
        }
      }
      return null;
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
