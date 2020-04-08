<template>
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
        <tr v-for="(row, i) in rows" :key="row">
          <td class="bg-gray">{{ i + 1 }}</td>
          <td v-for="(col, j) in columns" :key="col">
            <input type="text" @click="onCellClicked(i, j)" />
          </td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>

<script>
export default {
  data() {
    return {
      columns: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L'],
      rows: [...Array(12)],
      squares: [...Array(12)].map(r => Array(12).fill(0))
    }
  },
  created() {},
  methods: {
    onCellClicked(i, j) {
      console.log(this.squares[i][j], i, j)
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
</style>
