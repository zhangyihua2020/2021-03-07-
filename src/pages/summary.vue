<template>
  <div class="picture">
    <div class="oakboss">
      <span>{{ loginConfig.systemName }}</span>
      <a href="#" class="oakboss_font" @click="back">
        <img src="../assets/images/out.png" alt="" />
        <span class="out">退出登录</span>
      </a>
    </div>
    <div class="fou">
      <div
        class="four f"
        v-show="flag1 == loginConfig.divShow1"
        @mouseenter.stop="enter"
        @mouseleave.stop="leave"
        :class="{ show: change }"
      >
        <div :class="{ hide: change }">
          <img class="img" src="../assets/images/administer.png" alt="" />
          <span class="font">平台管理</span>
        </div>
        <div class="platform margin" v-show="change">
          <router-link to="/UserAssets" class="platform-money a">
            <img src="../assets/images/money.png" alt="" />
            <span>会员资产</span>
          </router-link>
          <router-link to="/merchantAsset/dataBoard">
            <div class="platform-money a">
              <img src="../assets/images/pos.png" alt="" />
              <span>商户资产</span>
            </div>
          </router-link>
          <router-link to="/financialManagement/dataBoard">
            <div class="platform-money a">
              <img src="../assets/images/finance.png" alt="" />
              <span>财务管理</span>
            </div>
          </router-link>
          <router-link to="/departmentAndRoleManagement/departmentManagement">
            <div class="platform-money a">
              <img src="../assets/images/human.png" alt="" />
              <span>人力资源</span>
            </div>
          </router-link>
          <router-link to="/Promotional" class="platform-money a">
            <img src="../assets/images/discount.png" alt="" />
            <span>促销优惠</span>
          </router-link>
          <router-link to="/System" class="platform-money a">
            <img src="../assets/images/system.png" alt="" />
            <span>系统运维</span>
          </router-link>
          <router-link to="/union" class="platform-money a">
            <img src="../assets/images/centre.png" alt="" />
            <span>物联中心</span>
          </router-link>
          <div class="ban">
            <img src="../assets/images/service.png" alt="" />
            <span>客户服务</span>
          </div>
        </div>
      </div>
      <div
        class="four f"
        v-show="flag2 == loginConfig.divShow2"
        @mouseenter.stop="enter1"
        @mouseleave.stop="leave1"
        :class="{ show: change1 }"
      >
        <div :class="{ hide: change1 }">
          <img class="img" src="../assets/images/electric.png" alt="" />
          <span class="font">智慧充电</span>
        </div>
        <div class="platform" v-show="change1">
          <router-link to="/summary/carCharging" class="platform-money a">
            <img src="../assets/images/Car battery.png" alt="" />
            <span>汽车充电</span>
          </router-link>
          <router-link to="/summary/motorcycles">
            <div class="platform-money a">
              <img src="../assets/images/Motorcycle battery.png" alt="" />
              <span>电单车充电</span>
            </div>
          </router-link>
          <div class="ban">
            <img src="../assets/images/Sharing the battery.png" alt="" />
            <span>共享电池</span>
          </div>
        </div>
      </div>
      <div
        class="four"
        v-show="flag3 == loginConfig.divShow3"
        @mouseenter.stop="enter2"
        @mouseleave.stop="leave2"
        :class="{ show: change2 }"
      >
        <div :class="{ hide: change2 }">
          <img class="img" src="../assets/images/stop.png" alt="" />
          <span class="font">智慧停车</span>
        </div>
        <div class="platform" v-show="change2">
          <router-link to="/wisdomParking" class="platform-money a">
            <img src="../assets/images/daolutingche.png" alt="" />
            <span>道路停车</span>
          </router-link>
          <router-link to="/parkingLot" class="platform-money a">
            <img src="../assets/images/tingchechang.png" alt="" />
            <span>停车场</span>
          </router-link>
          <div class="ban">
            <img src="../assets/images/gongxiangchewei.png" alt="" />
            <span>共享车位</span>
          </div>
        </div>
      </div>
      <div
        class="four f"
        v-show="flag4 == loginConfig.divShow4"
        @mouseenter.stop="enter3"
        @mouseleave.stop="leave3"
        :class="{ show: change3 }"
      >
        <div :class="{ hide: change3 }">
          <img class="img" src="../assets/images/use.png" alt="" />
          <span class="font">智慧用电</span>
        </div>
        <div class="platform" v-show="change3">
          <router-link to="/powerMonitorSystem/highVoltageRoom">
            <div class="platform-money a">
              <img src="../assets/images/Power monitoring.png" alt="" />
              <span>电力监控</span>
            </div>
          </router-link>
          <router-link to="/prepaidMeter/site">
            <div class="platform-money a">
              <img src="../assets/images/meter.png" alt="" />
              <span>预付费电表</span>
            </div>
          </router-link>
          <router-link to="/smartSocket/site">
            <div class="platform-money a">
              <img src="../assets/images/socket.png" alt="" />
              <span>智能插座</span>
            </div>
          </router-link>
        </div>
      </div>
      <div
        class="four f"
        v-show="flag5 == loginConfig.divShow5"
        @mouseenter.stop="enter4"
        @mouseleave.stop="leave4"
        :class="{ show: change4 }"
      >
        <div :class="{ hide: change4 }">
          <img class="img" src="../assets/images/foot.png" alt="" />
          <span class="font">智慧出行</span>
        </div>
        <div class="platform" v-show="change4">
          <router-link to="/vehicleDetectSystem/vehicle">
            <div class="platform-money a">
              <img src="../assets/images/Vehicle monitoring.png" alt="" />
              <span>车辆监测</span>
            </div>
          </router-link>
          <div class="ban">
            <img src="../assets/images/gongxiangqiche.png" alt="" />
            <span>共享汽车</span>
          </div>
          <div class="ban">
            <img src="../assets/images/gongxiangdanche.png" alt="" />
            <span>共享单车</span>
          </div>
          <div class="ban">
            <img src="../assets/images/wangyueche.png" alt="" />
            <span>网约车</span>
          </div>
        </div>
      </div>
      <div
        class="four"
        v-show="flag6 == loginConfig.divShow6"
        @mouseenter.stop="enter5"
        @mouseleave.stop="leave5"
        :class="{ show: change5 }"
      >
        <div :class="[{ hide: change5 }]">
          <img class="img" src="../assets/images/city.png" alt="" />
          <span class="font">智慧城市</span>
        </div>
        <div class="platform" v-show="change5">
          <router-link to="/smartCommunity/community">
            <div class="platform-money a">
              <img src="../assets/images/gongxiangqiche.png" alt="" />
              <span>智慧社区</span>
            </div>
          </router-link>
          <router-link to="/smartPark/park">
            <div class="platform-money a">
              <img src="../assets/images/gongxiangdanche.png" alt="" />
              <span>智慧园区</span>
            </div>
          </router-link>
          <div class="ban">
            <img src="../assets/images/wangyueche.png" alt="" />
            <span>智慧家庭</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { loginConfig } from "../config.js";
export default {
  data() {
    return {
      loginConfig,
      change: false,
      change1: false,
      change2: false,
      change3: false,
      change4: false,
      change5: false,
      flag1: true,
      flag2: true,
      flag3: true,
      flag4: true,
      flag5: true,
      flag6: true
    };
  },
  methods: {
    back() {
      this.$router.push({
        path: "/"
      });
      window.document.cookie = "userName" + "=" + "";
      window.document.cookie = "pas" + "=" + "";
      localStorage.removeItem("token");
    },
    enter() {
      this.change = true;
    },
    leave() {
      this.change = false;
    },
    enter1() {
      this.change1 = true;
    },
    leave1() {
      this.change1 = false;
    },
    enter2() {
      this.change2 = true;
    },
    leave2() {
      this.change2 = false;
    },
    enter3() {
      this.change3 = true;
    },
    leave3() {
      this.change3 = false;
    },
    enter4() {
      this.change4 = true;
    },
    leave4() {
      this.change4 = false;
    },
    enter5() {
      this.change5 = true;
    },
    leave5() {
      this.change5 = false;
    }
  }
};
</script>

<style scoped>
.a:hover {
  background: #63c8fb;
}

.xiao {
  background: #1e69fe !important;
}

.margin {
  margin-top: 40px !important;
  top: -5% !important;
}

.show {
  /* opacity: 50%; */
  background-color: #8fd8fd !important;
}

.hide {
  display: none;
}

.platform {
  width: 361px;
  height: 137.4px;
  margin: 0 auto;
  position: relative;
  top: 31%;
  left: 1%;
  transform: translate(0%, -50%);
  position: relative;
}

.platform-money:nth-child(n + 4) {
  margin-top: 20px;
}

.ban {
  margin-right: 12px;
  display: inline-block;
  background: white;
  height: auto;
  width: 72px;
  border-radius: 10px;
  position: relative;
  top: 50%;
  background-color: #ccc;
}

.ban img {
  width: 22px !important;
  height: 22px !important;
  margin-top: 10px !important;
}

.ban span {
  display: block;
  font-size: 12px;
  font-family: "PingFang SC";
  font-weight: 400;
  color: #000000;
  margin-top: -18px;
}

.platform-money {
  margin-right: 12px;
  display: inline-block;
  background: white;
  height: auto;
  width: 72px;
  border-radius: 10px;
  position: relative;
  top: 50%;
}

.platform-money img {
  width: 22px !important;
  height: 22px !important;
  margin-top: 10px !important;
}

.platform-money span {
  display: block;
  font-size: 12px;
  font-family: "PingFang SC";
  font-weight: 400;
  color: #000000;
  margin-top: -18px;
}

.oakboss_font img {
  width: 18px;
  height: 18px;
  margin-top: -5px;
  margin-right: 4px;
}

.oakboss_font {
  float: right;
  margin-right: 90px;
}

.oakboss {
  width: 100%;
  /* height: 30px; */
  margin-top: 34px;
  margin-left: 46px;
}

.oakboss span:nth-child(1) {
  font-size: 30px;
  font-family: "PingFang SC";
  font-weight: 400;
  color: #000000;
}

.out {
  font-size: 18px;
  font-family: "PingFang SC";
  font-weight: 400;
  color: #000000;
  clear: both;
}

.picture {
  background: url("../assets/images/bgm.png") no-repeat center;
  width: 100%;
  height: 100%;
  background-size: cover;
  position: fixed;
  top: 0;
  left: 0;
  margin: 0 auto;
  position: absolute;
  overflow-x: hidden;
}

.four {
  border-radius: 20px;
  width: 357px;
  height: 235px;
  background: #e0f8ff;
  text-align: center;
  line-height: 50px;
  position: relative;
  cursor: pointer;
  margin: 10px 20px 10px 20px;
}

.four .img {
  width: 118px !important;
  height: 118px !important;
  margin-top: 40px !important;
  margin: 0 auto;
}

.fou {
  display: flex;
  width: 1200px;
  height: 530px;
  flex-direction: row;
  flex-wrap: wrap;
  align-items: center;
  margin: 0 auto;
  margin-top: 7%;
  /* width: 1143px;
		height: 519px;

		position: relative;
		top: 44%;
		left: 50%;
		transform: translate(-50%, -50%); */
}

.font {
  font-size: 24px;
  font-family: PingFang SC;
  font-weight: 400;
  color: #000000;
  display: block;
}
</style>
