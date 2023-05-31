<template>
  <div>

    <el-row>
      <el-card >
        <el-col :span="3.1">
          <el-card style="weight:100px">
            <el-table :data="tableData" border stripe :header-cell-class-name="'headerBg'"  @selection-change="handleSelectionChange">
              <el-table-column prop="id" label="标签ID" width="80"></el-table-column>
              <el-table-column prop="name" label="标签名称" width="140"></el-table-column>
            </el-table>
          </el-card>
        </el-col>

        <div style="text-align: center">
          <el-card style="height: 650px">
            <div id="main" :style="{width: '88%', height: '600px'}"></div>
          </el-card>
        </div>
      </el-card>
    </el-row>

  </div>
</template>

<script>
import * as echarts from "echarts";

export default {
  name: "Tag",
  data() {
    return {
      tableData: [],
      total: 0,
      pageNum: 1,
      pageSize: 15,
      id: "",
      name: "",
      form: {},
      dialogFormVisible: false,
      multipleSelection: [],
      selectTagData :{}
    }
  },
  created() {
    this.load()
  },
  mounted() { //页面元素渲染之后再触发
    this.request.get("/echarts/selectTagData").then(res => {
      res.data.forEach(item =>{
        option.series[0].data.push({name:item.tagName, value:item.tagSum})
        myChart.setOption(option)
      })
    })
    var chartDom = document.getElementById('main');
    var myChart = echarts.init(chartDom);
    var option;

    option = {
      title: {
        text: '标签统计',
        left: '620px'
      },
      legend: {//底部数据
        top: 'bottom',
        left: '950px',
      },
      tooltip: {
        trigger: 'item'
      },
      toolbox: {//数据视图、还原、下载
        show: true,
        feature: {
          mark: { show: true },
          dataView: { show: true, readOnly: false },
          restore: { show: true },
          saveAsImage: { show: true }
        },
      },
      series: [
        {
          name: 'Nightingale Chart',
          type: 'pie',
          radius: [50, 250],
          center: ['50%', '50%'],
          roseType: 'area',
          itemStyle: {
            borderRadius: 5
          },
          data: [
          ]
        }
      ]
    };
  },
  methods: {
    load() {
      this.request.get("/tag/page", {
        params: {
          pageNum: this.pageNum,
          pageSize: this.pageSize,
          id: this.id,
          name: this.name
        }
      }).then(res => {
        this.tableData = res.data.records
        this.total = res.data.total
      })
    },
    handleSelectionChange(val) {
      console.log(val)
      this.multipleSelection = val
    },
    reset() {
      this.id = ""
      this.name = ""
      this.load()
    }
  }
}
</script>


<style>

</style>
