<template>
  <div id="app">
    <div class="header">
      <h1>{{ pageTitle }}</h1>
    </div>
    <div class="content">
      <div class="left-panel">
        <h2>左侧面板</h2>
        <button class="button">{{ leftPanelItems[0] }}</button>
        <button class="button">{{ leftPanelItems[1] }}</button>
        <button class="button">{{ leftPanelItems[2] }}</button>      
      </div>
      <div class="right-panel">
        <div class="top-right-box">上
          <!-- 新添加的表格 -->
          <div class="centered-table">

            <table id="dataofUser" border="1">
              <tr>
                <td>材料种类</td>
                <td>材料化学式</td>
                <td>材料结构式</td>
                <td>材料使用频率</td>
                <td><button @click="addColumn">添加列</button></td>
              </tr>
              <tr v-for="row in tableData" :key="row.id">
                <td><input type="text" v-model="row.category"></td>
                <td><input type="text" v-model="row.chemicalFormula"></td>
                <td><input type="text" v-model="row.structureFormula"></td>
                <td><input type="text" v-model="row.usageFrequency"></td>
                <td v-for="column in columns" :key="column.id">
                  <input type="text" v-model="row[column.property]">
                </td>
              </tr>
            </table>
            <button class="first-button" @click="addRow">添加行</button>
            <button @click="saveData">保存信息</button>
            <button @click="deleteLastSavedData">删除上一次保存的内容</button>
          </div>
        </div>

        <div class="bottom-right-box">
          <div class="left-bottom-box">左下<EchartsDemo1></EchartsDemo1></div>
          <div class="right-bottom-box">右下<EchartsDemo2></EchartsDemo2></div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { ref, onMounted, defineComponent } from "vue";
import EchartsDemo1 from "./view/EchartsDemo1.vue";
import EchartsDemo2 from "./view/EchartsDemo1.vue";

defineComponent({
  EchartsDemo1,
  EchartsDemo2
});
const EchartsDemo1Ref = ref();
const EchartsDemo2Ref = ref();
  data() {
    return {
      pageTitle: '数据库建造及呈现',
      leftPanelItems: ['项目1', '项目2', '项目3'],
      rightPanelText: '这是右侧面板的内容。',
      tableData: JSON.parse(localStorage.getItem("tableData")) || [], // 新添加的表格数据
      nextRowId: 1, // 用于生成唯一行标识的属性
      columns: [
        { id: 1, label: "材料种类", property: "category" },
        { id: 2, label: "材料化学式", property: "chemicalFormula" },
        { id: 3, label: "材料结构式", property: "structureFormula" },
        { id: 4, label: "材料使用频率", property: "usageFrequency" }
      ],
      tableData: [
        // 初始化的表格数据
        { id: 1, category: "", chemicalFormula: "", structureFormula: "", usageFrequency: "" },
        { id: 2, category: "", chemicalFormula: "", structureFormula: "", usageFrequency: "" }
      ],
      lastSavedData: [],
    };
  },

  methods: {
    addRow() {
      this.tableData.push({
        id: this.nextRowId++,
        category: '',
        chemicalFormula: '',
        structureFormula: '',
        usageFrequency: ''
      });
    },
    addColumn() {
      // 生成唯一的列 ID
      const newColumnId = this.columns.length + 1;

      // 添加新列的定义
      const newColumn = { id: newColumnId, label: `新列${newColumnId}`, property: `newColumn${newColumnId}` };
      this.columns.push(newColumn);

      // 在表格数据中为新列添加默认值
      this.tableData.forEach(row => {
        row[newColumn.property] = "";
      });
    },

    saveData() {
      localStorage.setItem("tableData", JSON.stringify(this.tableData));
      alert("表格数据已保存！");
    },
    deleteLastSavedData() {
      // 恢复表格数据为上一次保存的数据备份
      this.tableData = JSON.parse(JSON.stringify(this.lastSavedData));
    },
  },

};
</script>

<style scoped>
.header {
  background-color: rgb(117, 113, 113);
  padding: 20px;
  text-align: center;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.3); 
}

.content {
  display: flex;
  flex: 1 7;
}

.left-panel {
  flex: 1;
  background-color: rgba(14, 10, 10, 0.164);
  padding: 20px;
  height: 1600px;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.3); 
}

.right-panel {
  flex: 6; /* 右侧占6/7 */
  background-color: rgb(255, 255, 255);
  padding: 20px;
  display: flex;
  flex-direction: column;
}

.top-right-box {
  flex: 1; /* 上部占1/4 */
  background-color: rgb(255, 255, 255);
  margin: 10px;
  border: 1px solid rgb(170, 210, 249);
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.3); 
}

.centered-table {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.first-button{
  align-items:flex-end;
}


.bottom-right-box {
  flex: 3; /* 下部占3/4 */
  display: flex;
}

.left-bottom-box {
  flex: 1; /* 左下占1/2 */
  background-color: rgb(255, 255, 255);
  margin: 10px;
  border: 1px solid rgb(170, 210, 249);
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.3); 
}

.right-bottom-box {
  flex: 1; /* 右下占1/2 */
  background-color: rgb(255, 255, 255);
  margin: 10px;
  border: 1px solid rgb(170, 210, 249);
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.3); 
}

.button {
  width: 100%;
  padding: 10px;
  background-color: lightgray;
  border: 2px solid gray;
  text-align: center;
  cursor: pointer;
}
</style>