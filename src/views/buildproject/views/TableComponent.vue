<template>
  <div class="centered-table">
    <button @click="addRow">添加行</button>
    <table id="dataofUser" border="1">
      <tr>
        <td>材料种类</td>
        <td>材料化学式</td>
        <td>材料结构式</td>
        <td>材料使用频率</td>
      </tr>
      <tr v-for="row in tableData" :key="row.id">
        <td></td>
        <td></td>
        <td></td>
        <td></td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [],
      nextRowId: 1,
    };
  },
  methods: {
    addRow() {
      this.tableData.push({
        id: this.nextRowId++,
      });
    },
  },
};
</script>

<style scoped>
.centered-table {
  display: flex;
  flex-direction: column;
  align-items: center;
}

/* Add more styling as needed for your design */
</style>