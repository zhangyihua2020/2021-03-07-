<template>
  <div class="tem-right">
    <div class="tem-right-top">
      <div class="top-left">
        <div class="top-left-word">基础信息</div>
      </div>

      <div>
        <myhead></myhead>
      </div>
    </div>
    <div class="right-con">
      <div class="right-con-right">
        <headMsg></headMsg>
        <div>
          <!-- <div class="jichu">
            <div></div>
            <span>基础信息</span>
          </div>
          <div class="tu">
            <div @mouseenter="enter" @mouseleave="leave">
              <div class="zi" :class="{ zii: isgo }">
                <div class="zi_1" v-if="isgo">
                  <img src="../../assets/images/gen.png" alt="" />
                  <div>更换站点照片</div>
                </div>
              </div>
            </div>
            <div @mouseenter="enter2" @mouseleave="leave2">
              <div class="zi zs" :class="{ zii: isgos }">
                <div class="zi_1" v-if="isgos">
                  <img src="../../assets/images/gen.png" alt="" />
                  <div>更换二维码</div>
                </div>
              </div>
            </div>
          </div> -->
          <div class="jichu">
            <div></div>
            <span>站点信息</span>
          </div>
          <div>
            <div class="inp">
              <div>站点名称:</div>
              <div>
                <input
                  type="text"
                  v-model="input"
                  placeholder="请输入内容"
                  disabled="disabled"
                  class="jibenInput banInput"
                />
              </div>
            </div>
            <div class="inp">
              <div>类型:</div>
              <div>
                <input
                  type="text"
                  v-model="typeInput"
                  placeholder="充电桩"
                  disabled="disabled"
                  class="jibenInput banInput"
                />
              </div>
            </div>
            <div class="inp">
              <div>地址:</div>
              <div class="blueBorder">
                <input
                  type="text"
                  v-model="weiInput"
                  placeholder=""
                  class="jibenInput"
                />
              </div>
            </div>
            <!-- <div class="inp">
              <div>位置:</div>
              <img src="../../assets/images/tutu.png">
            </div> -->
            <div class="inp">
              <div>备注:</div>
              <textarea v-model="text" class="kuang"></textarea>
            </div>
            <div class="left">
              <el-button @click="clear" class="e">取消</el-button>
              <el-button class="e" type="primary" @click="xiu">保存</el-button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import myhead from "../../components/myhead";
import headMsg from "../../components/headMsg";
export default {
  components: {
    myhead,
    headMsg
  },
  data() {
    return {
      isgo: false,
      isgos: false,
      stationsId: "",
      input: "",
      typeInput: "",
      weiInput: "",
      text: ""
    };
  },
  created() {
    this.token = localStorage.getItem("token");
    this.stationsId = this.$store.state.id;
    this.getStationMes();

    if (this.$store.state.type == 1) {
      this.typeInput = "汽车充电C";
    } else if (this.$store.state.type == 4) {
      this.typeInput = "自行车棚";
    } else if (this.$store.state.type == 2) {
      this.typeInput = "停车场";
    } else if (this.$store.state.type == 3) {
      this.typeInput = "道路";
    }
  },
  methods: {
    getStationMes() {
      let toKen = this.token.replace(/\"/g, "");
      let url = `/admin/api/charger/${this.stationsId}?token=${toKen}`;
      this.$axios.get(url).then(res => {
        console.log("res.data.name");
        console.log(res.data);
        console.log(res.data.charger);
        this.input = res.data.charger.name;
        this.weiInput = res.data.charger.address;
        this.text = res.data.charger.memo;
      });
    },
    clear() {
      this.weiInput = "";
      this.text = "";
    },
    xiu() {
      let toKen = this.token.replace(/\"/g, "");
      let url = `/admin/api/charger/${this.stationsId}?token=${toKen}&address=${this.weiInput}&memo=${this.text}`;
      console.log("url");
      console.log(url);
      this.$axios.put(url).then(res => {
        console.log(res);
        // console.log(res.data.users)
        // console.log(res.status)//打印状态码
        if (res.status !== 200) {
          return this.$message.error("修改失败!");
        }
        this.$message.success("修改成功!");
        setTimeout(() => {
          this.getStationMes();
        }, 888);
      });
    },
    leave2() {
      this.isgos = false;
    },
    enter2() {
      this.isgos = true;
    },
    leave() {
      this.isgo = false;
    },
    enter() {
      this.isgo = true;
    }
  }
};
</script>

<style scoped="scoped">
.e {
  width: 10%;
}

.jibenInput {
  border-radius: 4px;
  border: 1px solid #dcdfe6;
  height: 40px;
  line-height: 40px;
  outline: 0;
  padding: 0 15px;
  width: 370px;
}

.banInput {
  cursor: no-drop;
}

.blueBorder input:focus {
  border-style: solid;
  border-color: #1e69fe;
}

.el-input {
  width: 199%;
}

.left {
  margin: 20px 0 0 150px;
}

.kuang {
  width: 400px;
  height: 150px;
  border: 1px #ccc solid;
  resize: none;
  border-radius: 5px;
}

.inp > div:nth-child(1) {
  font-size: 20px;
  margin-right: 10px;
  width: 110px;
  text-align: center;
}

.inp {
  display: flex;
  margin: 23px 0 0 30px;
  align-items: center;
}

.zs {
  text-align: center;
}

.zi_1 {
  position: relative;
  top: 30%;
}

.zii {
  background: black;
  opacity: 0.8;
  display: block;
  border-radius: 30px;
}

.zi {
  height: 100%;
  font-size: 20px;
  font-family: PingFang SC;
  font-weight: 300;
  width: 100%;
  color: #ffffff;
}

.tu > div:nth-child(1) {
  display: flex;
  align-items: center;
  text-align: center;
  width: 150px;
  height: 150px;
  margin-right: 74px;
  background: url("../../assets/images/road.png") no-repeat;
  background-size: 100%, 100%;
}

.tu > div:nth-child(2) {
  width: 150px;
  height: 150px;
  margin-right: 74px;
  background: url("../../assets/images/img_30.jpg") no-repeat;
  background-size: 100%, 100%;
}

.tu {
  margin: 43px 61px 0 30px;
  display: flex;
}

.jichu {
  display: flex;
  margin-top: 30px;
  align-items: center;

  font-size: 20px;
}

.jichu div {
  border-radius: 50%;
  width: 15px;
  height: 15px;
  margin-right: 18px;
  background: #1e69fe;
}

.right-con-right {
  width: 100%;
  height: 100%;
}

.aa {
  margin-top: 41px !important;
}

.zhandian .el-button {
  padding: 0px !important;
}

.el-table td div {
  text-align: left;
}

.tem-right {
  /* height: 1217px !important; */
  display: flex;
  flex: 1;
  flex-direction: column;
  background-color: white;
  border-top-left-radius: 50px;
  border-bottom-left-radius: 50px;
}

.leftBox-con {
  display: flex;
  flex-direction: column;
  width: 40%;
}

.leftBox {
  display: flex;
  flex-direction: row;
}

.right-con-left {
  width: 30%;
  box-shadow: 10px 10px 15px #edf1f5;
}

.right-con {
  width: 95%;
  margin: 0 auto;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.road-bottom-right {
  width: 70%;
  text-align: right;
}

.road-bottom-left {
  width: 30%;
}

.tem-right-top {
  display: flex;
  flex-direction: row;
  width: 95%;
  margin: 20px auto;
  margin-top: 36px;
}

.right-con-top {
  width: 600px;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  margin: 15px 0 15px 0;
}

.top-left-word {
  font-family: PingFangSC-Regular;
  font-size: 24px;
  font-weight: normal;
  font-stretch: normal;
  line-height: 24px;
  letter-spacing: 1px;
  color: #000000;
}

.top-right {
  display: flex;
  width: 125px;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

.top-left {
  flex: 1;
  font-size: 24px;
  font-weight: 400;
  color: #000000;
}
</style>
