<script setup lang="ts">
import {ref} from "vue";

const moves = ref([]);

const currentMove = ref('');

const again = () => {
  for (let i = 0; i < 9; i++)  moves.value[i] = -1;
}

again();

const check = () => {
    let winner = null;
      if  (moves.value[0] !== -1 && (moves.value[0] === moves.value[1] && moves.value[0] === moves.value[2] ||
              moves.value[0] === moves.value[4] && moves.value[0] === moves.value[8] ||
              moves.value[0] === moves.value[3] && moves.value[0] === moves.value[6] ||
              moves.value[5] === moves.value[4] && moves.value[0] === moves.value[8]))
        winner = moves.value[0];
      else if (moves.value[4] !== -1 && (moves.value[2] === moves.value[4] && moves.value[2] === moves.value[6] ||
          moves.value[3] === moves.value[4] && moves.value[3] === moves.value[5] ||
          moves.value[1] === moves.value[4] && moves.value[1] === moves.value[7]))
        winner = moves.value[4];
      else if (moves.value[8] !== -1 && (moves.value[2] === moves.value[5] && moves.value[2] === moves.value[8] ||
          moves.value[6] === moves.value[7] && moves.value[6] === moves.value[8]))
        winner = moves.value[8];
      return winner;
}
const move = (item, move) => {
  moves.value[item - 1] = move;
  currentMove.value = move === 'x' ? 'x' : 'o';
  if(check()) alert("winner is " + check());
}
</script>

<template>
  <div class="field">
    <div v-for="item in moves.length">
      <div v-if="moves[item - 1] === -1">
        <button class="x" @click="move(item, 'x')" v-if="currentMove === 'o' || currentMove === ''">x</button>
        <button class="o" @click="move(item, 'o')" v-if="currentMove === 'x' || currentMove === ''">o</button>
      </div>
      <div v-else>
        {{moves[item - 1]}}
      </div>
    </div>
  </div>
  <button class="again" @click="again">again</button>
</template>

<style scoped>
.field{
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-template-rows: repeat(3, 100px);
  border: 1px solid gray;
  padding: 5px;
}

.field > div {
  border: 1px solid gray;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
}

.field > button {
  background: none;
}

.again {
  background: #ababab;
  margin-top: 10px;
}

</style>
