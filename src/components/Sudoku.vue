<script setup lang="ts">
import { ref } from 'vue'

// 初始化 9x9 的數獨網格
const grid = ref(Array(9).fill(null).map(() => Array(9).fill('')))
</script>

<template>
  <div class="sudoku-container">
    <div class="sudoku-grid">
      <div v-for="(row, rowIndex) in grid" :key="rowIndex" class="sudoku-row">
        <div
          v-for="(cell, colIndex) in row"
          :key="colIndex"
          class="sudoku-cell"
          :class="{
            'border-right': (colIndex + 1) % 3 === 0 && colIndex < 8,
            'border-bottom': (rowIndex + 1) % 3 === 0 && rowIndex < 8
          }"
        >
          <input
            type="text"
            v-model="grid[rowIndex][colIndex]"
            maxlength="1"
            class="cell-input"
            @input="e => validateInput(e, rowIndex, colIndex)"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.sudoku-container {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;
}

.sudoku-grid {
  border: 2px solid #333;
  display: inline-block;
  background-color: white;
}

.sudoku-row {
  display: flex;
}

.sudoku-cell {
  width: 50px;
  height: 50px;
  border: 1px solid #ccc;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}

.border-right {
  border-right: 2px solid #333;
}

.border-bottom {
  border-bottom: 2px solid #333;
}

.cell-input {
  width: 100%;
  height: 100%;
  border: none;
  text-align: center;
  font-size: 1.5rem;
  outline: none;
  background: transparent;
}

.cell-input:focus {
  background-color: #e8f0fe;
}
</style>

<script lang="ts">
function validateInput(event: Event, rowIndex: number, colIndex: number) {
  const input = event.target as HTMLInputElement
  // 只允許輸入 1-9 的數字
  const value = input.value
  if (!/^[1-9]$/.test(value)) {
    input.value = ''
  }
}
</script> 