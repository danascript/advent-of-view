<template>
  <div class="grid grid-cols-3 mb-5 text-sm">
    <button
      @click="onPlayerMove(cells[0].id)"
      class="h-[40px] w-[40px] leading-[40px] text-center border border-t-0 border-l-0"
    >
      {{ cells[0].content }}
    </button>
    <button @click="onPlayerMove(cells[1].id)" class="h-[40px] w-[40px] leading-[40px] text-center border border-t-0">
      {{ cells[1].content }}
    </button>
    <button
      @click="onPlayerMove(cells[2].id)"
      class="h-[40px] w-[40px] leading-[40px] text-center border border-t-0 border-r-0"
    >
      {{ cells[2].content }}
    </button>
    <button @click="onPlayerMove(cells[3].id)" class="h-[40px] w-[40px] leading-[40px] text-center border border-l-0">
      {{ cells[3].content }}
    </button>
    <button @click="onPlayerMove(cells[4].id)" class="h-[40px] w-[40px] leading-[40px] text-center border">
      {{ cells[4].content }}
    </button>
    <button @click="onPlayerMove(cells[5].id)" class="h-[40px] w-[40px] leading-[40px] text-center border border-r-0">
      {{ cells[5].content }}
    </button>
    <button
      @click="onPlayerMove(cells[6].id)"
      class="h-[40px] w-[40px] leading-[40px] text-center border border-l-0 border-b-0"
    >
      {{ cells[6].content }}
    </button>
    <button @click="onPlayerMove(cells[7].id)" class="h-[40px] w-[40px] leading-[40px] text-center border border-b-0">
      {{ cells[7].content }}
    </button>
    <button
      @click="onPlayerMove(cells[8].id)"
      class="h-[40px] w-[40px] leading-[40px] text-center border border-b-0 border-r-0"
    >
      {{ cells[8].content }}
    </button>
  </div>

  <p>
    Player <span class="font-bold text-lg">{{ currentPlayer }}</span> turn
  </p>

  <button class="text-sm rounded p-2 mt-10 bg-emerald-300 hover:bg-emerald-200 hover:text-gray-700" @click="resetGame">
    Reset Game
  </button>
</template>

<!-- What we will need: -->
<!-- 1. Initial state, start trigger -->
<!-- 2. Keeping track of which player is playing -->
<!-- 3. Keeping track of the board and winning combinations -->
<!-- 4. Ending the game upon win or a tie -->
<!-- 5. Reset game - back to point 1 -->

<script>
import Game from '@/Game.vue'

const PLAYER_ONE = 'x'
const PLAYER_TWO = 'o'
const WINNING_COMBO = [
  [1, 4, 7],
  [2, 5, 8],
  [3, 6, 9],
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
  [1, 5, 9],
  [3, 5, 7],
]

export default {
  name: 'Game',

  data() {
    return {
      currentPlayer: PLAYER_ONE,
      cells: [
        {
          id: 1,
          content: null,
        },
        {
          id: 2,
          content: 'x',
        },
        {
          id: 3,
          content: null,
        },
        {
          id: 4,
          content: null,
        },
        {
          id: 5,
          content: null,
        },
        {
          id: 6,
          content: null,
        },
        {
          id: 7,
          content: null,
        },
        {
          id: 8,
          content: null,
        },
        {
          id: 9,
          content: null,
        },
      ],
    }
  },
  methods: {
    onPlayerMove(id) {
      if (!this.isCellEmpty(id)) return

      this.cells = this.cells.map(cell => {
        if (cell.id === id) {
          return { ...cell, content: this.currentPlayer }
        }
        return cell
      })

      this.changeTurn()
    },
    isCellEmpty(id) {
      const clickedCell = this.cells.find(cell => cell.id === id)
      return !clickedCell.content
    },
    changeTurn() {
      this.currentPlayer = this.currentPlayer === PLAYER_ONE ? PLAYER_TWO : PLAYER_ONE
    },
    resetGame() {
      this.cells = this.cells.map(cell => ({ ...cell, content: null }))
    },
  },
}
</script>

<!-- Winning combinations -->
