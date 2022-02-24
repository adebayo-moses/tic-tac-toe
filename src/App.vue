<script setup>
import { ref, computed } from 'vue';

const player =  ref ("x");
const board  = ref([

  ["", "", ""],
  ["", "", ""],
  ["", "", ""]
  ]);

const CalculateWinner = (squares) => {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}

const winner = computed(() => CalculateWinner(board.value.flat()));

const MakeMove = (x, y) => {
  if (winner.value) return

  if (board.value[y][x] !== "") return

  board.value[y][x] = player.value;

  player.value = player.value === "x" ? "o" : "x";
}

const ResetGame = () => {
  board.value = [
    ["", "", ""],
    ["", "", ""],
    ["", "", ""]
  ];
  player.value = "x";
}


</script>

<template>
 <h1>Hello World</h1>
</template>

<style>

</style>
