<template>
	<div class="tem-right">
		<div class="tem-right-top">
			<div class="top-left">
				<div class="top-left-word">
					汽车充电
				</div>
			</div>
			<div class="users-right">
				<myhead></myhead>
			</div>
		</div>
		<!-- 设备添加框 -->
		<div class="aaa">
			<el-dialog :title="name" :visible.sync="dialogVisible" width="30%">
				<el-form>
					<el-form-item label="名字:">
						<el-input v-model="a" class="addinput"></el-input>
					</el-form-item>
					<el-form-item label="机号:">
						<el-input v-model="b" class="addinput"></el-input>
					</el-form-item>
					<el-form-item label="编号:">
						<el-input v-model="c" class="addinput"></el-input>
					</el-form-item>
					<el-form-item label="类型:">
						<el-select v-model="value" placeholder="交流桩">
							<el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
							</el-option>
						</el-select>
					</el-form-item>
				</el-form>
				<span slot="footer" class="dialog-footer">
					<el-button @click="dialogVisible = false">取 消</el-button>
					<el-button type="primary" @click="flag = true">确 定</el-button>
				</span>
			</el-dialog>
			<!-- 设备确认 -->

			<el-dialog title="提示" :visible.sync="flag" width="30%">
				<span>确定修改或者添加？</span>
				<span slot="footer" class="dialog-footer">
					<el-button @click="flag = false">取 消</el-button>
					<el-button type="primary" @click="(flag = false), (dialogVisible = false), add()">确 定</el-button>
				</span>
			</el-dialog>
		</div>


		<div class="right-con">
			<div class="right-con-left">
				<div class="right-con-top">
					<div class="textBox">
						<img src="../../assets/images/search.png" class="sear-img">
						<el-input placeholder="请输入站点名" class="textWord" v-model="input1" clearable @keyup.enter.native="getInputMes"></el-input>
					</div>
					<div class="but-weizhi1">
						<el-button type="primary" icon="el-icon-plus" @click="(addDialogVisible1 = true),zhandiantianjia()">添加</el-button>
					</div>
				</div>
				<template>
					<el-table :data="tableData" stripe style="width:100%">
						<el-table-column>
							<template slot-scope="scope">
								<div class="leftBox" :class="{ BGactive:scope.row.id == isActive }" @click="changeBg(scope.row.id),getParksMes(scope.row.id),(scope.row.station)">
									<div class="parkimg">
										<img :src="img[scope.row.type]" />
									</div>
									<div class="leftBox-con">
										<div class="parkName">
											{{scope.row.name}}
										</div>
										<div class="parkAddress">
											<div v-if="scope.row.address == ''">地址未配置</div>
											<div v-else>{{scope.row.address}}</div>
										</div>
										<div class="parkIcon">
											<div>
												<span class="parkIcon-word">停车场</span>
											</div>
											<div>
												<span class="parkIcon-word">充电桩</span>
											</div>
											<div>
												<span class="parkIcon-word">金额</span>
											</div>
										</div>
									</div>
									<template v-if="scope.row.id == isActive">
										<div class="leftBox-right">
											<div title="修改" @click="xiugai(scope.row.id)">
												<img src="../../assets/images/xiu.png">
											</div>
											<div title="删除" @click="removeUserByID1(scope.row.id)">
												<img src="../../assets/images/shan2.png">
											</div>
											<router-link to="/stationscar">
												<div title="详情" @click="huodeid(scope.row.package,scope.row.id,scope.row.name,scope.row.type,scope.row.address,scope.row.memo,scope.row.lot_rate_group,scope.row.rate_group)">
													<img src="../../assets/images/lan.png">
												</div>
											</router-link>
										</div>
									</template>
									<template v-else>
										<div style="text-align: right;width: 20%;font-size: 30px;">
											...
										</div>
									</template>
								</div>
							</template>
						</el-table-column>
					</el-table>
				</template>
				<div class="UserAssets-bottom">
					<div class="road-bottom-left" :data="tableData">
						<span>共{{total}}条信息</span>
					</div>
					<div class="road-bottom-right">
						<el-pagination background :current-page.sync.number="pagenum" @current-change="handleCurrentChange" :page-size="pagesize"
						 layout="prev, pager, next" :total="total" small :pager-count='5'>
						</el-pagination>
					</div>
				</div>
			</div>
			<div class="right-con-right">
				<div class="sousuo">
					<div class="textBox-right">
						<img src="../../assets/images/search.png" class="sear-img">
						<el-input placeholder="请输入信息进行查找" v-model="input2" class="textWord" @keyup.enter.native="getRoadChargers"
						 clearable></el-input>
					</div>
					<div class="but-weizhi">
						<el-button type="primary" icon="el-icon-search" @click="getRoadChargers">搜索</el-button>
					</div>
					<div>
						<el-button type="success" icon="el-icon-circle-plus-outline" @click="(dialogVisible = true), names()">添加</el-button>
					</div>
				</div>
				<template>
					<el-table :data="parkList" stripe style="width:100%">
						<el-table-column prop="id" label="设备ID">
						</el-table-column>
						<el-table-column prop="name" label="名称">
						</el-table-column>
						<el-table-column label="类型">
							<template slot-scope="scope">
								<div style="text-align: center !important">
									{{ typeres[scope.row.type] }}
								</div>
							</template>
						</el-table-column>
						<el-table-column prop="mac" label="机号">
						</el-table-column>
						<el-table-column label="状态" prop="online">
							<template slot-scope="scope">
								<span v-if="scope.row.online == true">在线</span>
								<span v-else>离线</span>
							</template>
						</el-table-column>
						<el-table-column prop="address" label="操作">
							<template slot-scope="scope">
								<div class="operation">
									<div>
										<button type="text" @click="removeUserByID(scope.row.id)"><img title="删除" src="../../assets/images/delete.png" /></button>
									</div>
									<div>
										<el-button type="text" @click="(dialogVisible = true), id(scope.row.id)"><img title="修改" src="../../assets/images/compile.png" /></el-button>
									</div>
									<router-link to="/chargerscar">
										<div @click="huodeid(scope.row.package,scope.row.id,scope.row.name,scope.row.type,scope.row.address,scope.row.memo,scope.row.lot_rate_group,scope.row.rate_group,kong)">
											<img title="详情" style="height:14px;width:19px" src="../../assets/images/see.png">
										</div>
									</router-link>
								</div>
							</template>
						</el-table-column>
					</el-table>
				</template>
				<div class="UserAssets-bottom">
					<div class="road-bottom-left" :data="parkList">
						<span>共{{parkTotal}}条信息</span>
					</div>
					<div class="road-bottom-right">
						<el-pagination background :current-page.sync.number="newpark" @current-change="parksNumber" :page-size="pagepark"
						 layout="prev, pager, next" :total="parkTotal">
						</el-pagination>
					</div>
				</div>
			</div>
		</div>
		<!-- 添加设备 -->
		<el-dialog title="添加设备" :visible.sync="addDialogVisible" width="30%" @close="addDialogClosed">
			<el-form :model="addForm" :rules=" formRules" ref="addFormRef" label-width="80px">
				<el-form-item label="设备编号" prop="dev_id">
					<el-input v-model="addForm.dev_id" class="addinput"></el-input>
				</el-form-item>
				<el-form-item label="泊位" prop="name">
					<el-input v-model="addForm.name" class="addinput"></el-input>
				</el-form-item>
				<el-form-item label="机号" prop="mac">
					<el-input v-model="addForm.mac" class="addinput"></el-input>
				</el-form-item>
			</el-form>
			<span slot="footer" class="dialog-footer">
				<el-button @click="addDialogVisible = false">取 消</el-button>
				<el-button type="primary" @click="chargersUser">确 定</el-button>
			</span>
		</el-dialog>
		<!-- 修改设备 -->
		<el-dialog title="修改设备" :visible.sync="editDialogVisible" width="30%" @close="editDialogClosed">
			<el-form :model="editForm" :rules="formRules" ref="editFormRef" label-width="80px">
				<el-form-item label="设备编号" prop="dev_id">
					<el-input v-model="editForm.dev_id" class="addinput"></el-input>
				</el-form-item>
				<el-form-item label="泊位" prop="name">
					<el-input v-model="editForm.name" class="addinput"></el-input>
				</el-form-item>
				</el-form-item>
				<el-form-item label="机号" prop="mac">
					<el-input v-model="editForm.mac" class="addinput" disabled></el-input>
				</el-form-item>
			</el-form>
			<span slot="footer" class="dialog-footer">
				<el-button @click="editDialogVisible = false">取 消</el-button>
				<el-button type="primary" @click="editChargerInfo">确 定</el-button>
			</span>
		</el-dialog>
		<!-- 添加设备 -->
		<el-dialog title="添加设备" :visible.sync="addDialogVisible1" width="30%" @close="addDialogClosed1">
			<el-form :model="addForm1" :rules="formRules" ref="addFormRef1" label-width="80px">
				<el-form-item label="站点名" prop="name">
					<el-input v-model="addForm1.name" class="addinput"></el-input>
				</el-form-item>
				<el-form-item label="地址" prop="address">
					<el-input v-model="addForm1.address" class="addinput"></el-input>
				</el-form-item>
			</el-form>
			<span slot="footer" class="dialog-footer">
				<el-button @click="addDialogVisible1 = false">取 消</el-button>
				<el-button type="primary" @click="chargersUser1">确 定</el-button>
			</span>
		</el-dialog>

		<!-- 添加站点 -->

		<el-dialog title="修改设备" :visible.sync="addD" width="30%" @close="addDialogClosed1">
			<el-form :rules="formRules" ref="addFormRef1" label-width="80px">
				<el-form-item label="站点名">
					<el-input v-model="b" class="addinput"></el-input>
				</el-form-item>
				<el-form-item label="地址">
					<el-input v-model="a" class="addinput"></el-input>
				</el-form-item>
			</el-form>
			<span slot="footer" class="dialog-footer">
				<el-button @click="addD = false">取 消</el-button>
				<el-button type="primary" @click="sends">确 定</el-button>
			</span>
		</el-dialog>

	</div>
</template>

<script>
	import myhead from "../../components/myhead.vue";
	export default {
		components: {
			myhead,
		},
		data() {
			return {
				img: [
					require("../../assets/images/comprehensive.png"),
					require("../../assets/images/Charging pile.png"),
					require("../../assets/images/parking.png"),
					require("../../assets/images/Road parking.png"),
					require("../../assets/images/comprehensive.png"),
					require("../../assets/images/comprehensive.png"),
					require("../../assets/images/comprehensive.png"),
					require("../../assets/images/comprehensive.png"),
					require("../../assets/images/comprehensive.png"),
					require("../../assets/images/comprehensive.png"),
				],
				addD: false,
				typeres: ["sdf", "直流桩", "交流桩"],
				kong: 1,
				a: "",
				b: "",
				c: "",
				d: "",
				name: "",
				arr: [],
				total: 1,
				parkTotal: 0,
				isActive: 0,
				token: "",
				pagenum: 1, //分页
				pagesize: 6,
				changeId: [],
				pagepark: 20,
				newpark: 1, //分页
				tableData: [],
				getStation: "",
				parkList: [],
				getFristID: "",
				input1: "",
				input2: "",
				newpark2: 1,
				editForm: {},
				editForm1: {},
				value: "",
				dialogVisible: false,
				stations: false,
				addDialogVisible: false,
				addDialogVisible1: false,
				isType: false,
				flag: false,
				leftType: "",
				lest_id: "",
				editDialogVisible: false, //控制修改设备对话框显示隐藏
				editDialogVisible1: false, //控制修改设备对话框显示隐藏
				addForm: {
					token: localStorage.getItem("token").replace(/\"/g, ""),
					dev_id: "",
					name: "",
					mac: "",
					type: 7,
				}, //添加设备添加数据
				addForm1: {
					token: localStorage.getItem("token").replace(/\"/g, ""),
					name: "",
					address: "",
					type: 1,
				}, //添加设备添加数据
				//修改设备表单数据
				editFormRules: {
					dev_id: [{
							required: true,
							message: "请输入用户名",
							trigger: "blur",
						},
						{
							min: 3,
							max: 10,
							message: "用户名的长度在3~10个字符之间",
							trigger: "blur",
						},
					],
					name: [{
							required: true,
							message: "请输入用户名",
							trigger: "blur",
						},
						{
							min: 3,
							max: 10,
							message: "用户名的长度在3~10个字符之间",
							trigger: "blur",
						},
					],
					mac: [{
							required: true,
							message: "请输入用户名",
							trigger: "blur",
						},
						{
							min: 3,
							max: 10,
							message: "用户名的长度在3~10个字符之间",
							trigger: "blur",
						},
					],
				},
				editFormRules1: {
					name: [{
							required: true,
							message: "请输入站点名",
							trigger: "blur",
						},
						{
							min: 3,
							max: 20,
							message: "站点名的长度在3~20个字符之间",
							trigger: "blur",
						},
					],
				},
				//添加表单的验证规则
				addFormRules: {
					dev_id: [{
							required: true,
							message: "请输入用户名",
							trigger: "blur",
						},
						{
							min: 3,
							max: 10,
							message: "用户名的长度在3~10个字符之间",
							trigger: "blur",
						},
					],
					name: [{
							required: true,
							message: "请输入用户名",
							trigger: "blur",
						},
						{
							min: 3,
							max: 10,
							message: "用户名的长度在3~10个字符之间",
							trigger: "blur",
						},
					],
					mac: [{
							required: true,
							message: "请输入用户名",
							trigger: "blur",
						},
						{
							min: 3,
							max: 10,
							message: "用户名的长度在3~10个字符之间",
							trigger: "blur",
						},
					],
					address: [{
							required: true,
							message: "地址",
							trugger: "blur",
						},
						{
							trigger: "blur",
						},
					],
				},
	   formRules: {
        dev_id: [
          {
            required: true,
            message: "设备编号不能为空",
            trigger: "blur"
          }
        ],
        name: [
          {
            required: true,
            message: "名称不能为空",
            trigger: "blur"
          }
        ],
        mac: [
          {
            required: true,
            message: "机号不能为空",
            trigger: "blur"
          }
        ],
        address: [
          {
            required: true,
            message: "地址不能为空",
            trugger: "blur"
          }
        ]
      },	
				options: [{
						value: "选项1",
						label: "直流桩",
					},
					{
						value: "选项2",
						label: "交流桩",
					},
				],
				selType: "",
			};
		},
		created() {
			this.token = localStorage.getItem("token");
			this.getRoadMes();
			// this.getRoadChargers()
			setTimeout(() => {
				this.getRoadChargers();
			}, 1000);
		},
		methods: {
			huodeid(xitong, id, name, type, address, memo, lot_rate_group, rate_group, kong) {
				if (kong == 1) {
					console.log('you');
					console.log(kong);
				}
				if (!kong == 1) {
					console.log('zuo');
					console.log(kong);
				}
				this.$store.commit("changeId", {
					chanId: id,
					name: name,
					type: type,
					address: address,
					memo: memo,
					lot_rate_group: lot_rate_group,
					rate_group: rate_group,
					kong: kong,
					xitong: xitong
				});
			},
			zhandiantianjia() {
				this.a = "";
				this.b = "";
				this.c = "";
				this.d = "";
			},
			sends() {
				let toKen = this.token.replace(/\"/g, "");
				this.$axios
					.put(
						"/admin/api/station/" +
						this.station_ids +
						"?token=" +
						toKen +
						"&name=" +
						this.a +
						"&address=" +
						this.b +
						"&type=1"
					)
					.then((res) => {
						console.log(res);
						if (res.data.error == 0) {
							this.addD = false;
							this.$message.success("修改站点成功");
							setTimeout(() => {
								this.getRoadMes();
							}, 2000);
						} else {
							this.$message.error("修改站点失败");
						}
					});
			},
			xiugai(station_id) {
				this.addD = true;
				this.station_ids = station_id;
				this.name = "修改站点";
			},
			getRoadMes() {
				//token去掉引号
				let toKen = this.token.replace(/\"/g, "");
				// console.log(toKen)
				this.$axios
					.get(
						"/admin/api/stations/1?token=" +
						toKen +
						"&page=" +
						this.pagenum +
						"&row=6"
					)
					.then((res) => {
						if (res.status == 200) {
							const {
								stations: result
							} = res.data; //用户列表数据
							this.tableData = result;
							this.total = res.data.total;
							this.getFristID = this.tableData[0].id;
							this.isActive = this.tableData[0].id;
							console.log(this.tableData);
						}
					});
			},
			names() {
				console.log("232");

				this.name = "添加设备";
			},
			changeBg(id) {
				this.isActive = id;
			},

			getInputMes() {
				//token去掉引号
				let toKen = this.token.replace(/\"/g, "");
				// console.log(toKen)
				this.$axios
					.get(
						"admin/api/stations?token=" +
						toKen +
						"&page=" +
						this.pagenum +
						"&row=6&keyword=" +
						this.input1
					)
					.then((res) => {
						if (res.status == 200) {
							this.tableData = res.data.stations; //用户列表数据
							this.total = res.data.total;
							// console.log(this.tableData)
						}
					});
			},

			getParksMes(id) {
				//token去掉引号
				this.getFristID = id;
				this.leftType = id;
				let toKen = this.token.replace(/\"/g, "");
				this.$axios
					.get(
						"admin/api/station/" +
						id +
						"/chargers?token=" +
						toKen +
						"&page=" +
						this.newpark +
						"&row=14"
					)
					.then((res) => {
						//console.log(id)
						console.log(res);
						if (res.status == 200) {
							this.parkList = res.data.chargers; //用户列表数据
							this.parkTotal = res.data.total;
							this.isType = true;
							console.log(this.getFristID);
						}
					});
			},
			getRoadChargers() {
				//token去掉引号
				let toKen = this.token.replace(/\"/g, "");
				// console.log(toKen)
				this.$axios
					.get(
						"admin/api/station/" +
						this.getFristID +
						"/chargers?token=" +
						toKen +
						"&page=" +
						this.newpark +
						"&row=14&keyword=" +
						this.input2
					)
					.then((res) => {
						console.log(res.data);
						if (res.status == 200) {
							this.parkList = res.data.chargers; //用户列表数据
							this.parkTotal = res.data.total;
							// console.log(this.tableData)
						}
					});
			},
			//点击确认按钮，添加新设备
			chargersUser() {
				let toKen = this.token.replace(/\"/g, "");
				this.$refs.addFormRef.validate((valid) => {
					if (!valid) {
						return this.$message.error("请输入正确的信息");
					} else {
						this.$axios
							.post(
								"/admin/api/charger?token=" +
								this.addForm.token +
								"&dev_id=" +
								this.addForm.dev_id +
								"&name=" +
								this.addForm.name +
								"&mac=" +
								this.addForm.mac +
								"&station=" +
								this.getFristID
							)
							.then((res) => {
								if (res.status !== 200) {
									return this.$message.error("添加信息失败!");
								}
								this.$message.success("添加信息成功!");
								this.addDialogVisible = false;
								console.log(this.addForm);
								console.log(res);
								//刷新用户列表
								setTimeout(() => {
									this.getRoadChargers();
								}, 1000);
							});
					} //若表单正则验证未通过，则不允许添加
				});
				//如果验证通过，则发起添加用户请求
			},
			chargersUser1() {
				let toKen = this.token.replace(/\"/g, "");
				this.$refs.addFormRef1.validate((valid) => {
					if (!valid) {
						return this.$message.error("请输入正确的信息");
					} else {
						this.$axios.post("/admin/api/station", this.addForm1).then((res) => {
							if (res.status !== 200) {
								return this.$message.error("添加信息失败!");
							}
							this.$message.success("添加信息成功!");
							this.addDialogVisible1 = false;
							setTimeout(() => {
								this.getRoadMes();
							}, 2000);
						});
					} //若表单正则验证未通过，则不允许添加
				});
				//如果验证通过，则发起添加用户请求
			},
			handleCurrentChange(newPage) {
				//console.log(newPage)
				this.pagenum = newPage;
				this.getRoadMes();
			},
			parksNumber(parknum) {
				this.newpark = parknum;
				if (this.isType) {
					this.getParksMes(this.leftType); //通过id查询右边数据
				} else {
					this.getRoadChargers(); //页面加载查询总数据
				}
			},
			//根据ID删除泊位
			async removeUserByID(id) {
				console.log(id);
				let toKen = this.token.replace(/\"/g, "");
				const confirmRes = await this.$confirm(
					"此操作将永久删除该信息, 是否继续?",
					"提示", {
						confirmButtonText: "确定",
						cancelButtonText: "取消",
						type: "warning",
					}
				).catch((err) => err);
				// console.log(confirmRes)
				if (confirmRes !== "confirm") {
					return this.$message.info("已取消删除");
				}
				this.$axios
					.delete("/admin/api/charger/" + id + "?token=" + toKen)
					.then((res) => {
						console.log(res.status);
						if (res.status == 200) {
							this.$message.success("删除数据成功");
							setTimeout(() => {
								this.getRoadChargers(); //刷新设备数据
							}, 1000);
						} else {
							this.$message.error("删除数据失败");
						}
					});
				//删除设备提示
			},
			async removeUserByID1(id) {
				console.log(id);
				let toKen = this.token.replace(/\"/g, "");
				const confirmRes1 = await this.$confirm(
					"此操作将永久删除该信息, 是否继续?",
					"提示", {
						confirmButtonText: "确定",
						cancelButtonText: "取消",
						type: "warning",
					}
				).catch((err) => err);
				// console.log(confirmRes)
				if (confirmRes1 !== "confirm") {
					return this.$message.info("已取消删除");
				}
				this.$axios
					.delete("/admin/api/station/" + id + "?token=" + toKen)
					.then((res) => {
						console.log(res.status);
						if (res.status == 200) {
							this.$message.success("删除数据成功");
							setTimeout(() => {
								this.getRoadMes(); //刷新设备数据
								this.getRoadChargers();
							}, 2000);
							console.log(this.tableData);
						} else {
							this.$message.error("删除数据失败");
						}
					});
				//删除设备提示
			},
			//点击修改，将选择的id查询到的数据渲染到修改文本框
			showEditDialog(id) {
				this.editDialogVisible = true;
				//token去掉引号
				let toKen = this.token.replace(/\"/g, "");
				// console.log(toKen)
				this.$axios
					.get("admin/api/charger/" + id + "?token=" + toKen + "&attach=state") //根据id点击修改的id查询设备信息
					.then((res) => {
						//console.log(res.status)
						if (res.status == 200) {
							this.editForm = res.data.charger;
							console.log(res.data.charger);
						}
					});
			},
			showEditDialog1(id) {
				this.editDialogVisible1 = true;
				//token去掉引号
				let toKen = this.token.replace(/\"/g, "");
				// console.log(toKen)
				this.$axios
					.get("admin/api/station/" + id + "?token=" + toKen) //根据id点击修改的id查询设备信息
					.then((res) => {
						//console.log(res.status)
						if (res.status == 200) {
							this.editForm1 = res.data.station;
						}
					});
			},

			//提交修改后的设备信息
			editChargerInfo() {
				let toKen = this.token.replace(/\"/g, "");
				this.$refs.editFormRef.validate((valid) => {
					if (!valid) {
						return this.$message.error("请输入正确的信息");
					} else {
						if (confirm("确认修改吗?")) {
							this.$axios
								.put("/admin/api/charger/" + this.editForm.id, {
									token: toKen,
									dev_id: this.editForm.dev_id,
									name: this.editForm.name,
									address: this.editForm.address,
									mac: this.editForm.mac,
								})
								.then((res) => {
									if (res.status !== 200) {
										return this.$message.error("设备修改失败!");
									}
									this.$message.success("设备修改成功!");
									this.addDialogVisible = false;
									//刷新设备列表
									setTimeout(() => {
										this.getRoadChargers();
									}, 1000);
									//关闭对话框
									this.editDialogVisible = false;
								});
						}
					} //若表单正则验证未通过，则不允许添加
				});
				//如果验证通过，则发起添加修改设备请求
			},
			//提交修改后的设备信息
			editChargerInfo1() {
				let toKen = this.token.replace(/\"/g, "");
				this.$refs.editFormRef1.validate((valid) => {
					if (!valid) {
						return this.$message.error("请输入正确的信息");
					} else {
						if (confirm("确认修改吗?")) {
							this.$axios
								.put("/admin/api/station/" + this.editForm1.id, {
									token: toKen,
									name: this.editForm1.name,
									address: this.editForm1.address,
								})
								.then((res) => {
									if (res.status !== 200) {
										return this.$message.error("设备站点失败!");
									}
									this.$message.success("设备站点成功!");
									this.addDialogVisible1 = false;
									console.log(this.editForm1);
									//刷新设备列表
									setTimeout(() => {
										this.getRoadMes(); //刷新设备数据
									}, 1000);
									//关闭对话框
									this.editDialogVisible1 = false;
								});
						}
					} //若表单正则验证未通过，则不允许添加
				});
				//如果验证通过，则发起添加修改设备请求
			},
			//添加设备对话框关闭事件
			addDialogClosed1() {
				this.$refs.addFormRef1.resetFields();
			},
			addDialogClosed() {
				this.$refs.addFormRef.resetFields();
			},
			//修改设备对话框关闭事件
			editDialogClosed() {
				this.$refs.editFormRef.resetFields();
			},
			editDialogClosed1() {
				this.$refs.editFormRef1.resetFields();
			},
			id(e) {
				this.lest_id = e;
				this.name = "修改设备";
				this.value = "交流桩";
			},
			names() {
				this.name = "添加设备";
			},
			add() {
				if (this.value == "选项1") {
					this.value = 1;
				} else {
					this.value = 2;
				}
				console.log(this.value);
				let toKen = this.token.replace(/\"/g, "");
				if (this.lest_id) {
					console.log("输出的是id");
					this.$axios
						.put(
							"/admin/api/charger/" +
							this.lest_id +
							"?token=" +
							toKen +
							"&name=" +
							this.a +
							"&mac=" +
							this.b +
							"&dev_id=" +
							this.c +
							"&type=" +
							this.value
						)
						.then((res) => {
							if (res.data.error == 0) {
								this.$message.success("修改设备成功");
								this.getRoadChargers();
							} else {
								this.$message.error("修改设备失败");
							}
						});
					this.lest_id = "";
					this.value = "交流桩";
					this.a = "";
					this.b = "";
					this.c = "";
					this.d = "";
				} else {
					this.name = "添加设备";
					console.log(this.name);

					console.log("输出的是添加");

					this.$axios
						.post(
							"/admin/api/charger?token=" +
							toKen +
							"&name=" +
							this.a +
							"&mac=" +
							this.b +
							"&dev_id=" +
							this.c +
							"&type=" +
							this.value +
							"&station=" +
							this.getFristID
						)
						.then((res) => {
							console.log(res);
							if (res.data.error == 0) {
								this.$message.success("添加设备成功");

								this.getRoadChargers();
							} else {
								this.$message.error("添加设备失败");
							}
							console.log(res.data.error);
						});
					this.value = "交流桩";
					this.a = "";
					this.b = "";
					this.c = "";
					this.d = "";
				}
			},
		},
	};
</script>

<style scoped="scoped">
	.UserAssets-bgcolor .el-button--primary {
		background: #1e69fe;
	}

	.el-select {
		border: 1px solid #1e69fe !important;
		width: 33%;
	}

	.el-table td div {
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
	}

	.el-form>>>.el-form-item__label {
		width: 96px !important;
		text-align: center;
	}

	.tem-right {
		display: flex;
		flex: 1;
		width: 80%;
		flex-direction: column;
		background-color: white;
		border-top-left-radius: 50px;
		border-bottom-left-radius: 50px;
	}

	.parkIcon-word {
		width: 38px;
		height: 13px;
		font-family: PingFangSC-Regular;
		font-size: 13px;
		font-weight: normal;
		font-stretch: normal;
		line-height: 20px;
		letter-spacing: 0px;
		color: #5f6062;
	}

	.BGactive {
		background-color: #bed3ff;
	}

	.sousuo {
		display: flex;
		flex-direction: row;
	}

	.leftBox-right {
		/* width: 20%; */
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		position: absolute;
		right: 14px;
		top: 0;
	}

	.leftBox-right div {
		margin-left: 8px;
		margin-top: 10px;
	}

	.parkIcon {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		text-align: center;
	}

	.parkIcon div {
		background-color: #f2d0bd;
		height: 22px;
		width: 55px;
		line-height: 22px;
		border-radius: 5px;
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

	.leftBox-con {
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
		display: flex;
		flex-direction: column;
		width: 45%;
		text-align: left;
		line-height: 35px;
	}

	.leftBox {
		display: flex;
		flex-direction: row;
	}

	::v-deep .el-select>.el-input {
		border-radius: 10px;
	}

	/* 弹出对话框边框样式 */
	.addinput {
		border: solid #1c6ff9 1px;
		border-radius: 10px;
		width: 70%;
	}

	.right-con-left {
		width: 26%;
		box-shadow: 1px 1px 20px 10px #edf1f5;
		height: 800px;
		border-radius: 10px;
	}

	.but-weizhi1 {
		margin-left: 10px;
	}

	.right-con-right {
		width: 68%;
	}

	.el-button--success {
		margin-left: 20px;
		border-radius: 10px;
		height: 37px;
		color: #1e69fe;
		background-color: #fff;
		border-color: #1e69fe;
		width: 100px;
	}

	.parkimg {
		margin: 13px 20px;
	}

	.parkimg img {
		width: 78px;
		height: 78px;
	}

	.el-table .cell {
		line-height: 44px;
	}

	.right-con {
		width: 95%;
		margin: 0 auto;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
	}

	.road-bottom-right {
		width: 65%;
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

	.textBox-right {
		width: 70%;
		height: 34px;
		border-radius: 10px;
		border: solid 1px #1e69fe;
		display: -webkit-box;
		display: -ms-flexbox;
		display: flex;
		-webkit-box-orient: horizontal;
		-webkit-box-direction: normal;
		-ms-flex-direction: row;
		flex-direction: row;
		-webkit-box-align: center;
		-ms-flex-align: center;
		align-items: center;
		-ms-flex-pack: distribute;
	}

	.right-con-top {
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		margin-top: 15px;
	}

	.but-weizhi {
		margin-left: 20px;
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
	}

	.textBox {
		width: 60%;
	}

	.sear-img {
		width: 15px;
		height: 15px;
		margin-left: 10px;
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
</style>
