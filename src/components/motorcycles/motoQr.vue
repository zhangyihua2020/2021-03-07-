<template>
  <div class="oneCard-right">
    <div class="UserAssets-right-top">
      <div class="user-left">
        <span class="user-word">扫码套餐</span>
      </div>
      <div class="users-right">
        <myhead></myhead>
      </div>
    </div>
    <div class="UserAssets-right-text">
      <div class="textBox">
        <img src="../../assets/images/search.png" class="sear-img" />
        <el-input
          v-model="input2"
          placeholder="请输入关键字进行查找"
          class="textWord"
          clearable
        ></el-input>
      </div>
      <div>
        <el-button type="primary" icon="el-icon-search" @click="getUserMes"
          >搜索</el-button
        >
      </div>
      <div>
        <el-button
          type="success"
          icon="el-icon-circle-plus-outline"
          @click="addDialogVisible = true"
          >添加</el-button
        >
      </div>
    </div>
    <div>
      <template>
        <el-table :data="menuList" stripe style="width: 95%">
          <el-table-column prop="id" label="套餐ID"> </el-table-column>
          <el-table-column prop="name" label="名称"> </el-table-column>
          <el-table-column prop="pay" label="价格/元"> </el-table-column>i'x
          <el-table-column prop="duration" label="时长/分"> </el-table-column>
          <el-table-column prop="type" label="类型" :formatter="formatterType">
          </el-table-column>
          <el-table-column prop="address" label="操作" width="200">
            <template slot-scope="scope">
              <div class="operation">
                <div>
                  <button type="text" @click="removeUserByID(scope.row.id)">
                    <img src="../../assets/images/delete.png" />
                  </button>
                </div>
                <div>
                  <button type="text" @click="showEditDialog(scope.row.id)">
                    <img src="../../assets/images/compile.png" />
                  </button>
                </div>
              </div>
            </template>
          </el-table-column>
        </el-table>
      </template>
    </div>
    <div class="UserAssets-bottom">
      <div class="UserAssets-bottom-left" :data="menuList">
        <span>共{{ total }}条信息</span>
      </div>
      <div class="UserAssets-bottom-right">
        <el-pagination
          background
          :current-page.sync.number="pagenum"
          @current-change="handleCurrentChange"
          :page-size="pagesize"
          layout="prev, pager, next"
          :total="total"
        >
        </el-pagination>
      </div>
    </div>
    <!-- 添加设备 -->
    <el-dialog
      title="添加套餐"
      :visible.sync="addDialogVisible"
      width="30%"
      @close="addDialogClosed"
    >
      <el-form
        :model="addForm"
        :rules="addFormRules"
        ref="addFormRef"
        label-width="80px"
      >
        <el-form-item label="名称" prop="name">
          <el-input v-model="addForm.name" class="addinput"></el-input>
        </el-form-item>
        <el-form-item label="价格/元" prop="pay">
          <el-input v-model="addForm.pay" class="addinput"></el-input>
        </el-form-item>
        <el-form-item label="时长/分" prop="duration">
          <el-input v-model="addForm.duration" class="addinput"></el-input>
        </el-form-item>
        <el-form-item label="类型:">
          <el-select v-model="addForm.type" placeholder="时间" disabled>
            <el-option label="电能" value="2"></el-option>
            <el-option label="时间" value="3"></el-option>
          </el-select>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="addDialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="chargersUser">确定</el-button>
      </span>
    </el-dialog>
    <!-- 修改设备 -->
    <el-dialog
      title="修改套餐"
      :visible.sync="editDialogVisible"
      width="30%"
      @close="editDialogClosed"
    >
      <el-form :model="editForm" ref="editFormRef" label-width="80px">
        <el-form-item label="名称" prop="name">
          <el-input v-model="addForm.name" class="addinput"></el-input>
        </el-form-item>
        <el-form-item label="价格" prop="pay">
          <el-input v-model="addForm.pay" class="addinput"></el-input>
        </el-form-item>
        <el-form-item label="时长" prop="duration">
          <el-input v-model="addForm.duration" class="addinput"></el-input>
        </el-form-item>
        <el-form-item label="类型:">
          <el-select v-model="addForm.type" placeholder="时间" disabled>
            <el-option label="电能" value="2" disabled></el-option>
            <el-option label="时间" value="3"></el-option>
          </el-select>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="editDialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="editChargerInfo">确定</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
import myhead from "../../components/myhead.vue";
export default {
  components: {
    myhead
  },
  data() {
    return {
      options: [
        {
          value: "选项1",
          label: "金额"
        },
        {
          value: "选项2",
          label: "电能"
        },
        {
          value: "选项3",
          label: "时间"
        }
      ],
      menuList: [], //卡数据
      userList: [], //这个是我新建的
      option: "",
      username: "",
      total: 1, //数据总条数
      isActive: true,
      dialogVisible: false,
      addDialogVisible: false,
      editDialogVisible: false, //控制修改设备对话框显示隐藏
      tcName: "",
      tcPay: "",
      tcDuration: "",
      tcType: "",
      add: false,
      selected: 0, //下拉框
      pagenum: 1, //分页
      token: "", //token令牌
      pagesize: 14, //每次查询条数
      type: 0,
      input: "",
      input2: "",
      editForm: {},
      typeList: [
        {
          id: 0,
          type: "所有"
        },
        {
          id: 1,
          type: "手机"
        },
        {
          id: 2,
          type: "微信"
        },
        {
          id: 3,
          type: "支付宝"
        }
      ],

      //修改套餐表单数据
      // editFormRules:{
      // 	title: [{
      // 		required: true,
      // 		message: '请输入信息',
      // 		trigger: 'blur'
      // 	}, {
      // 		min: 1,
      // 		max: 10,
      // 		message: '请输入正确的信息',
      // 		trigger: 'blur'
      // 	}],
      // 	pay: [{
      // 		required: true,
      // 		message: '请输入信息',
      // 		trigger: 'blur'
      // 	}, {
      // 		min: 1,
      // 		max: 10,
      // 		message: '请输入正确的信息',
      // 		trigger: 'blur'
      // 	}],
      // 	amount: [{
      // 		required: true,
      // 		message: '请输入信息',
      // 		trugger: 'blur'
      // 	}, {
      // 		min: 1,
      // 		max: 10,
      // 		message: '请输入正确的信息',
      // 		trigger: 'blur'
      // 	}]
      // },
      addForm: {
        token: localStorage.getItem("token").replace(/\"/g, ""),
        name: "",
        pay: "",
        type: "3",
        duration: "",
        source: "qr",
        service: 10,
        agent: 0,
        station: 0,
        charger: 0
      }, //添加设备添加数据
      addFormRules: {
        // name: [{
        // 	required: true,
        // 	message: '请输入信息',
        // 	trigger: 'blur'
        // }, {
        // 	min: 1,
        // 	max: 10,
        // 	message: '请输入正确的信息',
        // 	trigger: 'blur'
        // }],
        pay: [
          {
            required: true,
            message: "请输入信息",
            trigger: "blur"
          },
          {
            min: 1,
            max: 10,
            message: "请输入正确的信息",
            trigger: "blur"
          }
        ],
        duration: [
          {
            required: true,
            message: "请输入信息",
            trugger: "blur"
          },
          {
            min: 1,
            max: 10,
            message: "请输入正确的信息",
            trigger: "blur"
          }
        ]
      }
    };
  },
  created() {
    this.token = localStorage.getItem("token");
    this.getUserMes();
  },
  methods: {
    formatterType: function(row, column, cellValue) {
      var ret = ""; //你想在页面展示的值
      if (cellValue === 1) {
        ret = "金额"; //根据自己的需求设定
      } else if (cellValue === 2) {
        ret = "电能";
      } else if (cellValue === 3) {
        ret = "时间";
      } else {
        ret = "未知";
      }
      return ret;
    },
    handleOpen(key, keyPath) {},
    handleClose(key, keyPath) {},
    //获取用户卡信息列表
    getUserMes() {
      //token去掉引号
      let toKen = this.token.replace(/\"/g, "");
      if (!this.input2) {
        this.$axios
          .get(
            "/admin/api/packages/?token=" +
              toKen +
              "&page=" +
              this.pagenum +
              "&row=14&source=qr&service=10&agent=0&station=0&charger=0"
          )
          .then(res => {
            if (res.status == 200) {
              this.menuList = res.data.packages; //用户列表数据
              this.total = res.data.total;
            }
          });
      }

      this.$axios
        .get(
          "/admin/api/packages/?token=" +
            toKen +
            "&page=" +
            this.pagenum +
            "&row=14&source=qr&service=10&agent=0&station=0&charger=0&keyword=" +
            this.input2
        )
        .then(res => {
          if (res.status == 200) {
            this.menuList = res.data.packages; //用户列表数据
            this.total = res.data.total;
          }
        });
    },

    chargersUser() {
      let toKen = this.token.replace(/\"/g, "");
      this.$refs.addFormRef.validate(valid => {
        if (!valid) {
          return this.$message.error("请输入正确的信息");
        } else {
          this.$axios.post("/admin/api/package", this.addForm).then(res => {
            if (res.status !== 200) {
              return this.$message.error("添加失败!");
            }
            this.$message.success("添加成功!");
            this.addDialogVisible = false;
            //刷新用户列表
            setTimeout(() => {
              this.getUserMes();
            }, 1000);
          });
        } //若表单正则验证未通过，则不允许添加
      });
      //如果验证通过，则发起添加用户请求
    },
    async removeUserByID(id) {
      let toKen = this.token.replace(/\"/g, "");
      const confirmRes = await this.$confirm(
        "此操作将永久删除该套餐, 是否继续?",
        "提示",
        {
          confirmButtonText: "确定",
          cancelButtonText: "取消",
          type: "warning"
        }
      ).catch(err => err);
      if (confirmRes !== "confirm") {
        return this.$message.info("已取消删除");
      }
      this.$axios
        .delete("/admin/api/package/" + id + "?token=" + toKen) //,{"token:toKen"}
        .then(res => {
          if (res.status == 200) {
            this.$message.success("删除套餐成功");
            this.getUserMes(); //刷新用户数据
          } else {
            this.$message.error("删除套餐失败");
          }
        });
      //删除用户提示
    },
    //点击修改，将选择的id查询到的数据渲染到修改文本框
    showEditDialog(id) {
      this.editDialogVisible = true;
      //token去掉引号
      let toKen = this.token.replace(/\"/g, "");
      this.$axios
        .get("/admin/api/package/" + id + "?token=" + toKen) //根据id点击修改的id查询设备信息
        .then(res => {
          if (res.status == 200) {
            this.addForm.name = res.data.package.name;
            this.addForm.pay = res.data.package.pay;
            this.addForm.duration = res.data.package.duration;
            this.editForm = res.data.package;
          }
        });
    },

    //提交修改后的设备信息
    editChargerInfo() {
      let toKen = this.token.replace(/\"/g, "");
      var a = {
        token: toKen,
        pay: this.editForm.pay,
        duration: this.editForm.duration
      };

      console.log("对象");
      console.log(a);
      this.$refs.editFormRef.validate(valid => {
        if (!valid) {
          return this.$message.error("请输入正确的信息");
        } else {
          if (confirm("确认修改吗?")) {
            this.$axios
              .put("admin/api/package/" + this.editForm.id, this.addForm)
              .then(res => {
                if (res.status !== 200) {
                  return this.$message.error("修改失败!");
                }
                this.$message.success("修改成功!");
                this.addDialogVisible = false;
                //刷新设备列表
                setTimeout(() => {
                  this.getUserMes();
                }, 1000);

                //关闭对话框
                this.editDialogVisible = false;
              });
          }
        } //若表单正则验证未通过，则不允许添加
      });
      //如果验证通过，则发起添加修改设备请求
    },

    //监听页码值改变
    handleCurrentChange(newPage) {
      this.pagenum = newPage;
      this.getUserMes();
    },

    //添加套餐对话框关闭事件
    addDialogClosed() {
      this.$refs.addFormRef.resetFields();
    },

    //修改设备对话框关闭事件
    editDialogClosed() {
      this.$refs.editFormRef.resetFields();
    }
  }
};
</script>

<style scoped="scoped">
.oneCard-right {
  display: flex;
  flex: 1;
  flex-direction: column;
  background-color: white;
  border-top-left-radius: 50px;
  border-bottom-left-radius: 50px;
}

.el-table td {
  padding: 0 0;
}

.el-input__inner {
  height: 30px;
  border: none;
}

.tanchu {
  display: flex;
  flex-direction: row;
  align-items: center;
}

.tanchu-text {
  width: 248px;
  height: 17px;
  font-family: PingFangSC-Regular;
  font-size: 16px;
  font-weight: normal;
  font-stretch: normal;
  letter-spacing: 0px;
  color: #7b7b7b;
  margin-left: 5px;
}

.el-dialog {
  margin-top: 30vh !important;
}

.stateColor-red {
  color: red;
}

.stateColor-green {
  color: #2ec23c;
}

.active {
  background-color: white;
}

.operation {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  width: 70px;
  margin: 0 auto;
}

.el-table__footer-wrapper,
.el-table__header-wrapper {
  margin-top: 10px;
  background-color: #edf1f5;
}

.textWord {
  width: 390px;
  height: 30px;
  border: none;
}

/*  .is-opened>div::nth-child(1) {
	  background-color: white !important;
	} */

.cell {
  text-align: center;
  font-size: 15px;
  display: -webkit-box;
  overflow: hidden;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 1;
}

.el-table .cell {
  line-height: 44px;
}

.UserAssets-bgcolor {
  width: 100%;
  display: flex;
  flex-direction: row;
}

.UserAssets-right {
  display: flex;
  flex: 1;
  flex-direction: column;
  background-color: white;
  border-top-left-radius: 50px;
  border-bottom-left-radius: 50px;
}

/* 顶部按钮 */
.el-button--primary {
  border-radius: 10px;
  height: 37px;
}

.el-button--success {
  border-radius: 10px;
  height: 37px;
}

.el-button--default {
  border-radius: 10px;
  padding: 10px 20px;
}

.addinput {
  border: 1px solid #1e69fe;
  border-radius: 10px;
}

.el-table {
  color: #908e8e;
}

.UserAssets-right-top {
  display: flex;
  flex-direction: row;
  width: 95%;
  margin: 20px auto;
  margin-top: 40px;
}

.el-col-12 {
  width: 100%;
  text-align: center;
}

/* 字体 */
.vive {
  font-size: 20px;
  color: white;
  text-align: center;
  display: flex;
  flex-direction: row;
  margin: 20px 55px;
}

.el-submenu__title {
  font-size: 20px;
  width: 100%;
}

/* 按钮字体 */
.el-button {
  font-size: 16px;
  padding: 10px 20px;
}

.el-menu-item {
  font-size: 16px;
  color: #dbdbdb;
}

.menu-op {
  display: flex;
  flex-direction: row;
  width: 100%;
  margin-left: 8%;
}

.el-button {
  font-size: 16px;
  padding: 10px 20px;
}

.menu-op div {
  padding: 0px 15px;
  width: 40px;
}

.user-word {
  width: 47px;
  height: 23px;
  font-family: PingFangSC-Regular;
  font-size: 24px;
  font-weight: normal;
  font-stretch: normal;
  line-height: 24px;
  letter-spacing: 1px;
  color: #000000;
}

.el-button--primary {
  color: #fff;
  background-color: #1e69fe;
  border-color: #1e69fe;
}

.el-button--success {
  color: #1e69fe;
  background-color: #fff;
  border-color: #1e69fe;
}

.user-left {
  width: 50%;
}

.users-right-w {
  display: flex;
  flex-direction: row;
  align-items: center;
  width: 150px;
  justify-content: space-between;
  float: right;
}

.users-right {
  width: 50%;
}

.user-right span {
  color: #8a9199;
}

.user-img {
  height: 40px;
  width: 40px;
  overflow: hidden;
  border-radius: 100%;
}

.el-menu-item.is-active {
  border-radius: 400px;
  background-color: white !important;
}

.el-menu-item.is-active:hover {
  background-color: #1e69fe;
}

.UserAssets-right-text {
  width: 650px;
  margin-left: 40px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.select1 {
  width: 200px;
  height: 34px;
  border-radius: 10px;
  border: solid 1px #1e69fe;
  font-size: 16px;
  padding: 0 2%;
  margin: 0;
}

.textBox {
  width: 68%;
  height: 34px;
  border-radius: 10px;
  border: solid 1px #1e69fe;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-around;
}

.UserAssets-bottom {
  display: flex;
  flex-direction: row;
  width: 95%;
  margin: 29px auto;
}

.UserAssets-bottom-left {
  width: 50%;
}

.UserAssets-bottom-right {
  width: 50%;
  text-align: right;
}

.UserAssets-bottom-left span {
  width: 137px;
  height: 18px;
  font-family: PingFangSC-Regular;
  font-size: 16px;
  font-weight: 600;
  font-stretch: normal;
  line-height: 20px;
  letter-spacing: 0px;
  color: #333333;
}

.set {
  width: 40px;
}

.select1 option {
  text-align: center;
}

.sear-img {
  width: 15px;
  height: 15px;
  margin-left: 20px;
}

/* 第一行数据类型 */
.el-table thead {
  color: black;
}
</style>
