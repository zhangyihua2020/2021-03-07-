<template>
  <div class="UserAssets-bgcolor">
    <div class="UserAssets-left">
      <div class="UserAssets-logo">
        <router-link to="/summary">
          <img :src="loginConfig.imgs" />
        </router-link>
      </div>
      <!-- <div class="vive">
				<div class="set">
					<img src="../assets/images/Big Data View.png" />
				</div>
				<span>大数据视图</span>
			</div> -->
      <el-col :span="12">
        <el-menu
          default-active="2"
          class="el-menu-vertical-demo"
          @open="handleOpen"
          @close="handleClose"
          background-color="#1e69fe"
          text-color="#fff"
          active-text-color="white"
          unique-opened
          v-model="option"
        >
          <el-submenu index="1">
            <template slot="title">
              <div class="menu-op">
                <div>
                  <img src="../assets/images/user account.png" />
                </div>
                <span class="menu-word">数据视图</span>
              </div>
            </template>
            <el-menu-item-group>
              <el-menu-item index="6-1">
                <router-link to="/tccKanban">
                  <div class="menu-op">
                    <div>
                      <img src="../assets/images/all.png" />
                    </div>
                    <span class="menu-word">数据看板</span>
                  </div>
                </router-link>
              </el-menu-item>
              <el-menu-item index="6-2">
                <router-link to="/parkingLotRoadMap">
                  <div class="menu-op">
                    <div>
                      <img src="../assets/images/Monthly package.png" />
                    </div>
                    <span class="menu-word">全景图</span>
                  </div>
                </router-link>
              </el-menu-item>
            </el-menu-item-group>
          </el-submenu>
          <el-submenu index="2">
            <template slot="title">
              <div class="menu-op">
                <div>
                  <img src="../assets/images/berth.png" />
                </div>
                <span class="menu-word">套餐管理</span>
              </div>
            </template>
            <el-menu-item-group>
              <el-menu-item index="3-1">
                <router-link to="/Pbaoyue">
                  <div class="menu-op">
                    <div>
                      <img src="../assets/images/Monthly package.png" />
                    </div>
                    <span class="menu-word">包月套餐</span>
                  </div>
                </router-link>
              </el-menu-item>
            </el-menu-item-group>
          </el-submenu>
          <el-menu-item index="3">
            <template slot="title">
              <router-link to="/parkingChang">
                <div class="menu-op">
                  <div>
                    <img src="../assets/images/The parking lot.png" />
                  </div>
                  <span class="menu-word-2">停车场</span>
                </div>
              </router-link>
            </template>
          </el-menu-item>
          <el-menu-item index="4">
            <template slot="title">
              <router-link to="/jifeiguize">
                <div class="menu-op">
                  <div>
                    <img src="../assets/images/Accounting rules.png" />
                  </div>
                  <span class="menu-word-2">计费规则</span>
                </div>
              </router-link>
            </template>
          </el-menu-item>
          <el-submenu index="5">
            <template slot="title">
              <div class="menu-op">
                <div>
                  <img src="../assets/images/Parking record.png" />
                </div>
                <span class="menu-word">停车记录</span>
              </div>
            </template>
            <el-menu-item-group>
              <el-menu-item index="2-1">
                <router-link to="/AllparkCar">
                  <div class="menu-op">
                    <div>
                      <img src="../assets/images/all.png" />
                    </div>
                    <span class="menu-word">所有</span>
                  </div>
                </router-link>
              </el-menu-item>
              <el-menu-item index="2-2">
                <router-link to="/shishiParkCar">
                  <div class="menu-op">
                    <div>
                      <img src="../assets/images/Real-time parking.png" />
                    </div>
                    <span class="menu-word">实时停车</span>
                  </div>
                </router-link>
              </el-menu-item>
              <el-menu-item index="2-3">
                <router-link to="/hisParkCar">
                  <div class="menu-op">
                    <div>
                      <img src="../assets/images/The historical record.png" />
                    </div>
                    <span class="menu-word">历史记录</span>
                  </div>
                </router-link>
              </el-menu-item>
              <el-menu-item index="2-4">
                <router-link to="/qianfeiParkCar">
                  <div class="menu-op">
                    <div>
                      <img src="../assets/images/Payment records.png" />
                    </div>
                    <span class="menu-word">欠费记录</span>
                  </div>
                </router-link>
              </el-menu-item>
              <el-menu-item index="2-5">
                <router-link to="/yichangParkCar">
                  <div class="menu-op">
                    <div>
                      <img src="../assets/images/Abnormal records.png" />
                    </div>
                    <span class="menu-word">异常记录</span>
                  </div>
                </router-link>
              </el-menu-item>
              <el-menu-item index="2-6">
                <router-link to="/Insensitivee">
                  <div class="menu-op">
                    <div>
                      <img src="../assets/images/Non-inductive pay.png" />
                    </div>
                    <span class="menu-word">无感支付</span>
                  </div>
                </router-link>
              </el-menu-item>
            </el-menu-item-group>
          </el-submenu>
          <el-submenu index="6">
            <template slot="title">
              <div class="menu-op">
                <div>
                  <img src="../assets/images/berth.png" />
                </div>
                <span class="menu-word">统计报表</span>
              </div>
            </template>
            <el-menu-item-group>
              <el-menu-item index="5-1">
                <router-link to="/plYunYingBaoBiao">
                  <div class="menu-op">
                    <div>
                      <img src="../assets/images/Prepaid plan.png" />
                    </div>
                    <span class="menu-word">运营报表</span>
                  </div>
                </router-link>
              </el-menu-item>
              <el-menu-item index="5-2">
                <router-link to="/plYunYingShangBaoBiao">
                  <div class="menu-op">
                    <div>
                      <img src="../assets/images/Monthly package.png" />
                    </div>
                    <span class="menu-word">运营商报表</span>
                  </div>
                </router-link>
              </el-menu-item>
              <el-menu-item index="5-3">
                <router-link to="/plZhanDianBaoBiao">
                  <div class="menu-op">
                    <div>
                      <img src="../assets/images/Monthly package.png" />
                    </div>
                    <span class="menu-word">站点报表</span>
                  </div>
                </router-link>
              </el-menu-item>
            </el-menu-item-group>
          </el-submenu>
        </el-menu>
      </el-col>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import { loginConfig } from "../config.js";
export default {
  data() {
    return {
      loginConfig,
      titleName: "",
      roadName: "road",
      tableData: [], //用户数据
      userList: [], //这个是我新建的
      option: "",
      username: "",
      total: 1, //数据总条数
      isActive: true,
      dialogVisible: false,
      add: false,
      selected: 0, //下拉框
      pagenum: 1, //分页
      token: "", //token令牌
      pagesize: 14, //每次查询条数
      type: 0,
      input: ""
    };
  },
  created() {
    this.token = localStorage.getItem("token");
  },
  methods: {
    onChange(name, type) {
      this.titleName = name;
      this.roadName = type;
      console.log(this.roadName);
    },
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
      console.log(this.option);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    },
    //获取用户信息列表
    getRoadMes() {
      //token去掉引号
      let toKen = this.token.replace(/\"/g, "");
      // console.log(toKen)
      this.$axios
        .get(
          "/admin/api/roads/?token=" +
            toKen +
            "&page=" +
            this.pagenum +
            "&row=6"
        )
        .then(res => {
          console.log(res.data);
          // console.log(res.data.users)
          // console.log(res.status)//打印状态码
          if (res.status == 200) {
            this.tableData = res.data.roads; //用户列表数据
            this.total = res.data.total;
            // console.log(this.tableData)
            var pn = this.pagenum;
          }
        });
    },
    handleCurrentChange(newPage) {
      //console.log(newPage)
      this.pagenum = newPage;
      this.getUserMes();
    }
  }
};
</script>

<style>
body {
  background-color: #1e69fe;
}

.UserAssets-bgcolor .el-table td {
  padding: 0 0;
}

.UserAssets-bgcolor .el-input__inner {
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

.operation {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  width: 70px;
  margin: 0 auto;
}

.UserAssets-bgcolor .el-table__footer-wrapper,
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

.UserAssets-bgcolor .cell {
  text-align: center;
  font-size: 16px;
  display: -webkit-box;
  -webkit-line-clamp: 1;
  font-weight: 400;
}

.UserAssets-bgcolor .el-table .cell {
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

/* 菜单选项卡字体颜色 */
.menu-word {
  color: white;
}

/* 顶部按钮 */
.UserAssets-bgcolor .el-button--primary {
  border-radius: 10px;
  height: 37px;
}

.UserAssets-bgcolor .el-button--default {
  border-radius: 10px;
  padding: 10px 20px;
}

.UserAssets-bgcolor .el-table {
  color: #908e8e;
}

.UserAssets-right-top {
  display: flex;
  flex-direction: row;
  width: 95%;
  margin: 20px auto;
  margin-top: 40px;
}

.UserAssets-left {
  display: flex;
  flex-direction: column;
  min-width: 200px;
  background-color: #1e69fe;
}

.UserAssets-logo {
  text-align: center;
  margin: 30px 0px;
}

.LOGO {
  width: 67px;
  height: 20px;
  font-family: MyriadPro-Regular;
  font-size: 24px;
  font-weight: normal;
  font-stretch: normal;
  line-height: 44px;
  letter-spacing: 0px;
  color: #ffffff;
}

.UserAssets-bgcolor .el-col-12 {
  width: 100%;
  text-align: center;
}

/* 字体 */
.vive {
  font-size: 15px;
  color: white;
  text-align: center;
  display: flex;
  flex-direction: row;
  margin: 13px auto;
  width: 100%;
}

.UserAssets-bgcolor .el-submenu__title {
  font-size: 15px;
  width: 100%;
}

/* 按钮字体 */
.UserAssets-bgcolor .el-button {
  font-size: 16px;
}

.UserAssets-bgcolor .el-menu-item {
  font-size: 13px;
  color: #dbdbdb;
}

.menu-op {
  display: flex;
  flex-direction: row;
  width: 100%;
  margin: 0 auto;
}

.menu-op div {
  padding: 0px 6px;
  width: 40px;
}

.UserAssets-bgcolor .el-submenu__title i {
  color: white;
}

.user-word {
  font-family: PingFangSC-Regular;
  font-size: 15px;
  color: #000000;
}

.user-left {
  width: 50%;
}

.user-right {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
}

.user-right {
  width: 10%;
}

.menu-word-2 {
  color: white;
  font-size: 15px;
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

.el-menu-item.is-active:hover {
  background-color: #1e69fe;
}

.UserAssets-right-text {
  width: 39%;
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
  width: 422px;
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
  width: 30px;
  margin-left: 30px;
}

.vive span {
  margin-left: 10px;
}

.set img {
  width: 17px;
  height: 17px;
}

.select1 option {
  text-align: center;
}

.sear-img {
  width: 15px;
  height: 15px;
}

/* 第一行数据类型 */
.UserAssets-bgcolor .el-table thead {
  color: black;
}
</style>
