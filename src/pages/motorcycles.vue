<template>
  <div class="cyf">
    <div class="UserAssets-bgcolor">
      <div class="UserAssets-left">
        <div class="UserAssets-logo">
          <router-link to="/summary">
            <img :src="loginConfig.imgs" />
          </router-link>
        </div>

        <el-col :span="12">
          <el-menu
            default-active="2"
            class="el-menu-vertical-demo"
            background-color="#1e69fe"
            text-color="#fff"
            active-text-color="white"
            unique-opened
          >
            <el-submenu index="6">
              <template slot="title">
                <div class="menu-op">
                  <div>
                    <img src="../assets/images/Prepaid plan.png" />
                  </div>
                  <span class="menu-word">数据视图</span>
                </div>
              </template>
              <el-menu-item-group>
                <el-menu-item index="6-1">
                  <router-link to="/motoKanban">
                    <div class="menu-op">
                      <div>
                        <img src="../assets/images/all.png" />
                      </div>
                      <span class="menu-word">数据看板</span>
                    </div>
                  </router-link>
                </el-menu-item>
                <el-menu-item index="6-2">
                  <router-link tag="a" target="_blank" to="/motoBigData">
                    <div class="menu-op">
                      <div>
                        <img src="../assets/images/all.png" />
                      </div>
                      <span class="menu-word">大数据</span>
                    </div>
                  </router-link>
                </el-menu-item>
                <el-menu-item index="6-3">
                  <router-link to="/motoMap">
                    <div class="menu-op">
                      <div>
                        <img
                          src="../assets/images/Sweep the code package.png"
                        />
                      </div>
                      <span class="menu-word">全景图</span>
                    </div>
                  </router-link>
                </el-menu-item>
              </el-menu-item-group>
            </el-submenu>
            <el-submenu index="1">
              <template slot="title">
                <div class="menu-op">
                  <div>
                    <img src="../assets/images/Carport manage.png" />
                  </div>
                  <span class="menu-word">资源管理</span>
                </div>
              </template>
              <el-menu-item-group>
                <el-menu-item index="1-2">
                  <router-link to="/motoAll">
                    <div class="menu-op">
                      <div>
                        <img src="../assets/images/site.png" />
                      </div>
                      <span class="menu-word">车棚</span>
                    </div>
                  </router-link>
                </el-menu-item>
                <el-menu-item index="1-3">
                  <router-link to="/equipment">
                    <div class="menu-op">
                      <div>
                        <img src="../assets/images/Gateway device.png" />
                      </div>
                      <span class="menu-word">网关设备</span>
                    </div>
                  </router-link>
                </el-menu-item>
              </el-menu-item-group>
            </el-submenu>
            <el-submenu index="2">
              <template slot="title">
                <div class="menu-op">
                  <div>
                    <img src="../assets/images/The charging order.png" />
                  </div>
                  <span class="menu-word">充电订单</span>
                </div>
              </template>
              <el-menu-item-group>
                <el-menu-item index="2-1">
                  <router-link to="/motoOrder">
                    <div class="menu-op">
                      <div>
                        <img src="../assets/images/all.png" />
                      </div>
                      <span class="menu-word">所有</span>
                    </div>
                  </router-link>
                </el-menu-item>
                <el-menu-item index="2-2">
                  <router-link to="/motoReal">
                    <div class="menu-op">
                      <div>
                        <img src="../assets/images/Real-time order.png" />
                      </div>
                      <span class="menu-word">实时订单</span>
                    </div>
                  </router-link>
                </el-menu-item>
                <el-menu-item index="2-3">
                  <router-link to="/motoHistory">
                    <div class="menu-op">
                      <div>
                        <img src="../assets/images/Order history.png" />
                      </div>
                      <span class="menu-word">历史订单</span>
                    </div>
                  </router-link>
                </el-menu-item>
                <el-menu-item index="2-4">
                  <router-link to="/motoRefund">
                    <div class="menu-op">
                      <div>
                        <img src="../assets/images/RefundTrade.png" />
                      </div>
                      <span class="menu-word">退款订单</span>
                    </div>
                  </router-link>
                </el-menu-item>
              </el-menu-item-group>
            </el-submenu>
            <el-submenu index="3">
              <template slot="title">
                <div class="menu-op">
                  <div>
                    <img src="../assets/images/Prepaid plan.png" />
                  </div>
                  <span class="menu-word">预付费套餐</span>
                </div>
              </template>
              <el-menu-item-group>
                <!-- <el-menu-item index="3-1">
									<router-link to="/mototaocan">
										<div class="menu-op">
											<div>
												<img src="../assets/images/all.png" />
											</div>
											<span class="menu-word">所有</span>
										</div>
									</router-link>
								</el-menu-item> -->
                <el-menu-item index="3-2">
                  <router-link to="/motoQr">
                    <div class="menu-op">
                      <div>
                        <img
                          src="../assets/images/Sweep the code package.png"
                        />
                      </div>
                      <span class="menu-word">扫码套餐</span>
                    </div>
                  </router-link>
                </el-menu-item>
                <el-menu-item index="3-3">
                  <router-link to="/motoRfid">
                    <div class="menu-op">
                      <div>
                        <img src="../assets/images/Charge packag.png" />
                      </div>
                      <span class="menu-word">刷卡套餐</span>
                    </div>
                  </router-link>
                </el-menu-item>
              </el-menu-item-group>
            </el-submenu>
            <el-submenu index="5">
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
                  <router-link to="/motoBaobiao">
                    <div class="menu-op">
                      <div>
                        <img src="../assets/images/Prepaid plan.png" />
                      </div>
                      <span class="menu-word">运营报表</span>
                    </div>
                  </router-link>
                </el-menu-item>
                <el-menu-item index="5-2">
                  <router-link to="/motoOperators">
                    <div class="menu-op">
                      <div>
                        <img src="../assets/images/Monthly package.png" />
                      </div>
                      <span class="menu-word">运营商报表</span>
                    </div>
                  </router-link>
                </el-menu-item>
                <el-menu-item index="5-3">
                  <router-link to="/motoZhanDianBaoBiao">
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
            <!-- <el-submenu index="4">
							<template slot="title">
								<div class="menu-op">
									<div>
										<img src="../assets/images/Prepaid plan.png" />
									</div>
									<span class="menu-word">统计报表</span>
								</div>
							</template>
							<el-menu-item-group>
								<el-menu-item index="3-1">
									<router-link to="/carList">
										<div class="menu-op">
											<div>
												<img src="../assets/images/all.png" />
											</div>
											<span class="menu-word">资源报表</span>
										</div>
									</router-link>
								</el-menu-item>
								<el-menu-item index="3-2">
									<router-link to="/meal">
										<div class="menu-op">
											<div>
												<img src="../assets/images/Sweep the code package.png" />
											</div>
											<span class="menu-word">充电报表</span>
										</div>
									</router-link>
								</el-menu-item>
							</el-menu-item-group>
						</el-submenu> -->
          </el-menu>
        </el-col>
      </div>
      <router-view></router-view>
    </div>
  </div>
</template>
<script>
import { loginConfig } from "../config.js";
export default {
  data() {
    return {
      loginConfig
    };
  }
};
</script>
<style lang="stylus">
body {
	background-color: #1e69fe;
	height: 100%;
}

.cyf {
	.UserAssets-bgcolor .el-table td {
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

	/* .is-opened>div::nth-child(1) {
   background-color: white !important;
 } */
	.UserAssets-bgcolor .cell {
		text-align: center;
		font-size: 16px;
		display: -webkit-box;
		overflow: hidden;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 1;
		font-weight: 400;
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

	.UserAssets-left {
		display: flex;
		flex-direction: column;
		min-width: 200px;
		height: 935px;
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

	.el-col-12 {
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

	.el-submenu__title {
		font-size: 15px;
		width: 100%;
	}

	/* 按钮字体 */
	.el-button {
		font-size: 16px;
	}

	.el-menu-item {
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

	.el-submenu__title i {
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
		font-size: 15px;
		color: white;
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
	.el-table thead {
		color: black;
	}
}
</style>
