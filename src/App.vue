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
  <main class="pt-8 text-center dark:bg-gray-800 min-h-screen dark:text-white">
    <h1 class="mb-8 text 3xl font-bold uppercase">Tic Tac Toe</h1>

    <h3 class="text-xl mb-4"> Player {{ player }}'s Turn</h3>


<div class=".flex.flex-col.items items-center mb-8">
  <div
  v-for="(row, x) in board"
  :key="x"
  class="flex">
  
  <div
  v-for="(cell, y) in row"
  :key="y"
  @click="MakeMove(x, y)"
  :class="`border border-white w-20 h-20 hover:bg-gray-700 flex items-center justify-center material-icons-outlines text-4xl cursor-pointer ${ cell === 'X' ? 'text-pink-500' : 'text-blue-400'  }`">
  {{ cell === 'X' ? 'close' : cell === 'O' ? 'circle' : ' ' }}
  </div>

  
  </div>
</div>

<h2 class="text-6xl font-bold mb-8">Player '{{winner}}' wins!</h2>

<button @click="ResetGane" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Reset Game</button>

  </main>
</template>

<style>
body {
  @apply bg-gray-800 text-white;
}
</style>
