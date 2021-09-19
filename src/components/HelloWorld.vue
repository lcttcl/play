<template>

  <div class="hello">
    <div>
      <el-button @click="resetDateFilter">清除日期过滤器</el-button>
      <el-button @click="clearFilter">清除所有过滤器</el-button>
      <el-table
          ref="filterTable"
          :data="tableData"
          style="width: 100%">
        <el-table-column
            prop="date"
            label="日期"
            sortable
            width="180"
            column-key="date"
            :filters="[{text: '2016-05-01', value: '2016-05-01'}, {text: '2016-05-02', value: '2016-05-02'}, {text: '2016-05-03', value: '2016-05-03'}, {text: '2016-05-04', value: '2016-05-04'}]"
            :filter-method="filterHandler"
        >
        </el-table-column>
        <el-table-column
            prop="name"
            label="姓名"
            width="180">
        </el-table-column>
        <el-table-column
            prop="address"
            label="地址"
            :formatter="formatter">
        </el-table-column>
        <el-table-column
            prop="tag"
            label="标签"
            width="100"
            :filters="[{ text: '家', value: '家' }, { text: '公司', value: '公司' }]"
            :filter-method="filterTag"
            filter-placement="bottom-end">
          <template slot-scope="scope">
            <el-tag
                :type="scope.row.tag === '家' ? 'primary' : 'success'"
                disable-transitions>{{scope.row.tag}}</el-tag>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <vxe-table
        border
        height="400"
        :data="tableData0">
      <vxe-column type="seq" width="60"></vxe-column>
      <vxe-column field="name" title="Name"></vxe-column>
      <vxe-column field="sex" title="Sex"></vxe-column>
      <vxe-column field="age" title="Age"></vxe-column>
      <vxe-column field="address" title="Address" show-overflow></vxe-column>
    </vxe-table>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return {
      tableData0: [
        { id: 10001, name: 'Test1', role: 'Develop', sex: 'Man', age: 28, address: 'vxe-table 从入门到放弃' },
        { id: 10002, name: 'Test2', role: 'Test', sex: 'Women', age: 22, address: 'Guangzhou' },
        { id: 10003, name: 'Test3', role: 'PM', sex: 'Man', age: 32, address: 'Shanghai' },
        { id: 10004, name: 'Test4', role: 'Designer', sex: 'Women', age: 23, address: 'vxe-table 从入门到放弃' },
        { id: 10005, name: 'Test5', role: 'Develop', sex: 'Women', age: 30, address: 'Shanghai' },
        { id: 10006, name: 'Test6', role: 'Designer', sex: 'Women', age: 21, address: 'vxe-table 从入门到放弃' },
        { id: 10007, name: 'Test7', role: 'Test', sex: 'Man', age: 29, address: 'vxe-table 从入门到放弃' },
        { id: 10008, name: 'Test8', role: 'Develop', sex: 'Man', age: 35, address: 'vxe-table 从入门到放弃' },
        { id: 10009, name: 'Test9', role: 'Test', sex: 'Man', age: 26, address: 'vxe-table 从入门到放弃' },
        { id: 10010, name: 'Test10', role: 'Develop', sex: 'Man', age: 38, address: 'vxe-table 从入门到放弃' },
        { id: 10011, name: 'Test11', role: 'Test', sex: 'Women', age: 29, address: 'vxe-table 从入门到放弃' },
        { id: 10012, name: 'Test12', role: 'Develop', sex: 'Man', age: 27, address: 'vxe-table 从入门到放弃' },
        { id: 10013, name: 'Test13', role: 'Test', sex: 'Women', age: 24, address: 'vxe-table 从入门到放弃' },
        { id: 10014, name: 'Test14', role: 'Develop', sex: 'Man', age: 34, address: 'vxe-table 从入门到放弃' },
        { id: 10015, name: 'Test15', role: 'Test', sex: 'Man', age: 21, address: 'vxe-table 从入门到放弃' },
        { id: 10016, name: 'Test16', role: 'Develop', sex: 'Women', age: 20, address: 'vxe-table 从入门到放弃' },
        { id: 10017, name: 'Test17', role: 'Test', sex: 'Man', age: 31, address: 'vxe-table 从入门到放弃' },
        { id: 10018, name: 'Test18', role: 'Develop', sex: 'Women', age: 32, address: 'vxe-table 从入门到放弃' },
        { id: 10019, name: 'Test19', role: 'Test', sex: 'Man', age: 37, address: 'vxe-table 从入门到放弃' },
        { id: 10020, name: 'Test20', role: 'Develop', sex: 'Man', age: 41, address: 'vxe-table 从入门到放弃' }
      ],
      tableData: [{
        date: '2016-05-02',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄',
        tag: '家'
      }, {
        date: '2016-05-04',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1517 弄',
        tag: '公司'
      }, {
        date: '2016-05-01',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1519 弄',
        tag: '家'
      }, {
        date: '2016-05-03',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1516 弄',
        tag: '公司'
      }]

    }
  },
  methods: {
    resetDateFilter() {
      this.$refs.filterTable.clearFilter('date');
    },
    clearFilter() {
      this.$refs.filterTable.clearFilter();
    },
    formatter(row) {
      return row.address;
    },
    filterTag(value, row) {
      return row.tag === value;
    },
    filterHandler(value, row, column) {
      const property = column['property'];
      return row[property] === value;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
