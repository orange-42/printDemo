<template>
  <div>
    <!-- <ul class="print-ul">
            <li v-for="(item,index) of tableData" :key="index" 
                :id="'printDiv' + index" style="page-break-after:always;">
                <div>
                    <p>{{item.date}}</p>
                    <p>{{item.name}}</p>
                    <p>{{item.province}}</p>
                    <p>{{item.city}}</p>
                    <p>{{item.address}}</p>
                    <p>{{item.zip}}</p>
                </div>
            </li>
        </ul> -->
    <el-button
      type="primary"
      style="float: right; margin-bottom: 10px"
      size="small"
      @click="printVisiable = true"
      >打印</el-button
    >
    <table
      border="1"
      bordercolor="#ebeef5"
      cellpadding="0"
      cellspacing="0"
      style="page-break-after: always; margin: 5px 0; width: 100%"
    >
      <tr>
        <th>
          <input
            type="checkbox"
            value=""
            @click="chooseAll"
            :checked="allcheck"
          />
        </th>
        <th>日期</th>
        <th>名字</th>
        <th>省份</th>
        <th>城市</th>
        <th>地址</th>
        <th>压缩号码</th>
        <th>操作</th>
      </tr>
      <tr v-for="(item, index) in tableData" :key="index">
        <!-- :id="'printDiv' + index" -->

        <td>
          <input
            type="checkbox"
            @click="getList(item)"
            value="true"
            :checked="item.check"
          />
        </td>
        <td>{{ item.date }}</td>
        <td>{{ item.name }}</td>
        <td>{{ item.province }}</td>
        <td>{{ item.city }}</td>
        <td>{{ item.address }}</td>
        <td>{{ item.zip }}</td>
        <td>
          <el-button size="mini" type="primary" @click="edit(item)"
            >编辑</el-button
          ><el-button size="mini" type="danger">删除</el-button>
        </td>
      </tr>
    </table>
    <div>
      <el-dialog title="打印预览" :visible.sync="printVisiable">
        <div style="height:50vh;overflow:auto">
<div
          style="text-align: left;page-break-after: always; margin: 5px 0; width: 100%;"
          v-for="(it, i) in detailList"
          :key="i"
          :id="'printDiv' + i"
        >
          <pre>名字：{{ it.name }}</pre>
          <pre>省份：{{ it.province }}</pre>
          <pre>城市：{{ it.city }}</pre>
          <pre>地址：{{ it.address }}</pre>
          <pre>压缩号：{{ it.zip }}</pre>
        </div>
        </div>
        
        <div slot="footer" class="dialog-footer">
          <el-button @click="printVisiable = false">取 消</el-button>
          <el-button type="primary" @click="handlePrint">确 定</el-button>
        </div>
      </el-dialog>
    </div>
    <el-dialog title="收货地址" :visible.sync="dialogFormVisible">
      <div>
        <el-row :gutter="20">
          <el-col :span="6">
            <div><label>名字：</label>{{ form.name }}</div>
          </el-col>
          <el-col :span="6">
            <div><label>省份：</label>{{ form.province }}</div>
          </el-col>
          <el-col :span="6">
            <div><label>城市：</label>{{ form.city }}kg</div>
          </el-col>
          <el-col :span="6">
            <div><label>地址：</label>{{ form.address }}</div>
          </el-col>
        </el-row>
      </div>

      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogFormVisible = false"
          >确 定</el-button
        >
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dialogFormVisible: false,
      printVisiable: false,
      allcheck: false,
      detailList: [],
      form: {
        name: "",
        province: "",
        city: "",

        address: "",
      },
      tableData: [
        {
          date: "2016-05-03",
          name: "王小虎",
          province: "上海",
          city: "普陀区",
          address: "上海市普陀区金沙江路 1518 弄",
          zip: 200333,
          check: false,
        },
        {
          date: "2016-05-02",
          name: "王大陆",
          province: "上海",
          city: "普陀区",
          address: "上海市普陀区金沙江路 1518 弄",
          zip: 200333,
          check: false,
        },
        {
          date: "2016-05-04",
          name: "王老五",
          province: "上海",
          city: "普陀区",
          address: "上海市普陀区金沙江路 1518 弄",
          zip: 200333,
          check: false,
        },
        {
          date: "2016-05-01",
          name: "王老吉",
          province: "上海",
          city: "普陀区",
          address: "上海市普陀区金沙江路 1518 弄",
          zip: 200333,
          check: false,
        },
        {
          date: "2016-05-08",
          name: "王炸",
          province: "上海",
          city: "普陀区",
          address: "上海市普陀区金沙江路 1518 弄",
          zip: 200333,
          check: false,
        },
        {
          date: "2016-05-06",
          name: "王中王",
          province: "上海",
          city: "普陀区",
          address: "上海市普陀区金沙江路 1518 弄",
          zip: 200333,
          check: false,
        },
        {
          date: "2016-05-07",
          name: "指环王",
          province: "上海",
          city: "普陀区",
          address: "上海市普陀区金沙江路 1518 弄",
          zip: 200333,
          check: false,
        },
      ],
    };
  },
  methods: {
    edit(data) {
      this.form = data;
      this.dialogFormVisible = true;
    },
    chooseAll() {
      this.allcheck = !this.allcheck;
      for (var i = 0; i < this.tableData.length; i++) {
        if (this.allcheck == true) {
          this.tableData[i].check = true;
        } else {
          this.tableData[i].check = false;
        }
      }
    },
    getList(data) {
      this.detailList = [];
      data.check = !data.check;
      var arr = [];
      for (var i = 0; i < this.tableData.length; i++) {
        console.log(this.tableData[i].check);
        if (this.tableData[i].check == true) {
          this.detailList.push(this.tableData[i]);
        }
      }
      console.log(this.detailList, "this.detailList");
    },
    handlePrint() {
      this.printVisiable = false;
      var newWin = window.open(""); //新打开一个空窗口
      for (var i = 0; i < this.detailList.length; i++) {
        var imageToPrint = document.getElementById("printDiv" + i); //获取需要打印的内容
        console.log(imageToPrint, "imageToPrint");
        newWin.document.write(imageToPrint.outerHTML); //将需要打印的内容添加进新的窗口
      }
      const styleSheet = `<style>li{list-style:none}</style>`;
      newWin.document.head.innerHTML = styleSheet; //给打印的内容加上样式
      newWin.document.close(); //在IE浏览器中使用必须添加这一句
      newWin.focus(); //在IE浏览器中使用必须添加这一句
      setTimeout(function () {
        newWin.print(); //打印
        newWin.close(); //关闭窗口
      }, 100);
    },
  },
};
</script>

<style>
.print-ul {
  width: 600px;
  list-style: none;
  border: 1px solid #e8e8e8;
}
td {
  padding: 10px;
}
button {
  margin: 0 5px;
}
th {
  color: #909399;
  padding: 5px 0;
}
</style>