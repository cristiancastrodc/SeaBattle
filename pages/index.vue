<template>
  <div>
    <v-simple-table class="game-table">
      <template v-slot:default>
        <thead>
          <tr class="bg-gray">
            <th class="text-center"></th>
            <th class="text-center">A</th>
            <th class="text-center">B</th>
            <th class="text-center">C</th>
            <th class="text-center">D</th>
            <th class="text-center">E</th>
            <th class="text-center">F</th>
            <th class="text-center">G</th>
            <th class="text-center">H</th>
            <th class="text-center">I</th>
            <th class="text-center">J</th>
            <th class="text-center">K</th>
            <th class="text-center">L</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(row, i) in squares" :key="i">
            <td class="bg-gray">{{ i + 1 }}</td>
            <td
              v-for="(col, j) in squares[i]"
              :key="j"
              @click="onCellClicked(i, j)"
              :class="classes[i][j]"
            ></td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
    <div class="text-center">
      <v-bottom-sheet v-model="sheet">
        <v-sheet class="text-center pa-5" height="260px">
          <p class="display-1">{{ cellTitle }}</p>
          <v-btn block class="mb-3" color="primary" @click="setCell(-1)"
            >nada <v-icon>mdi-adjust</v-icon></v-btn
          >
          <v-btn block class="mb-3" color="success" @click="setCell(1)"
            >herido <v-icon>mdi-gamepad</v-icon></v-btn
          >
          <v-btn block class="mb-3" color="teal darken-4" @click="setCell(2)"
            >soldadito <v-icon>mdi-face</v-icon></v-btn
          >
          <v-btn block class="mb-3" color="error" @click="sheet = !sheet"
            >otro <v-icon>mdi-security</v-icon></v-btn
          >
        </v-sheet>
      </v-bottom-sheet>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      columns: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L'],
      rows: [...Array(12)],
      squares: [...Array(12)].map(r => Array(12).fill(0)),
      classes: [...Array(12)].map(r => Array(12).fill('')),
      sheet: false,
      currentI: null,
      currentJ: null
    }
  },
  methods: {
    onCellClicked(i, j) {
      if (this.squares[i][j] === 0) {
        this.sheet = true

        this.currentI = i
        this.currentJ = j
      }
    },
    setCell(value) {
      this.squares[this.currentI][this.currentJ] = value
      this.classes[this.currentI][this.currentJ] =
        value === -1 ? 'bg-blue' : value === 2 ? 'bg-green' : 'bg-red'
      this.$set(this.classes, this.currentI, this.classes[this.currentI])

      this.sheet = false
    }
  },
  computed: {
    cellTitle() {
      return this.currentI != null && this.currentCell != null
        ? `${this.currentJ}${this.currentI}`
        : `${this.columns[this.currentJ]}${this.currentI + 1}`
    }
  }
}
</script>

<style lang="scss">
.game-table {
  width: auto;

  .bg-gray {
    background-color: #cecece;
  }

  &.v-data-table td,
  &.v-data-table th {
    border: 1px solid gray;
    padding: 6.5px;
    height: 30px;
    text-align: center;
  }
}
.bg-red {
  background-color: #c35c5c;
}
.bg-blue {
  background-color: #77b9d6;
}
.bg-green {
  background-color: #49af6b;
}
</style>
