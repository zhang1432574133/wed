<template>
	<div>
		<div class="register_sex">
			<div class="sub" v-show="isshow ? true:false">
				<div class="tit"> 您是男神还是女神？</div>
				<div @click="showModal(true,item)" v-for="(item,i) in avaList" :key="item.id" style="margin-top:20px">
					<a href="javascript:;">
						<img :src="item.url" alt="">
					</a>
					<p class="ti1">{{item.text}}</p>
					<p>{{item.txt}}</p>
				</div>
			</div>
			<div v-show="isnext">
				<div class="loc_ti">以下是您所在位置，点击位置区域<br>进行修改</div>
				<mapDrag @drag="dragMap" lat="31.231706" lng="121.472644"></mapDrag>
				<form action="">
					<div>
						<div id="allmap">
							<div class="content-block">
								<input id="demo1" type="text" placeholder="城市选择" name="pro" v-model="select" @click="bottomCity">
								<input id="value1" type="hidden"> </div>
						</div>
						<div class="gearArea" v-show="cityShow">
							<div class="area_btn_box">
								<div class="area_btn larea_cancel" @click="cancle">取消</div>
								<div class="area_btn larea_finish" @click="ok">确定</div>
							</div>
						
							<mt-picker :slots="myAddressSlots" @change="onMyAddressChange"></mt-picker>
						</div>
					</div>
					<input class="btn" type="button" value="下一步" @click="enterDate">
				</form>
			</div>
			<div class="register" v-show="dateShow">
				<div v-if="dateModal">
					<div class="ti1">
						<img :src="src" alt="" style="">
					</div>
					<div style="font-size:14px;color:#999;text-align:center;margin-bottom:20px;">请选择您的出生年月</div>
					<mt-datetime-picker v-model="pickerVisible" type="date" @confirm="handleConfirm" year-format="{value} 年" month-format="{value} 月" date-format="{value} 日" :startDate="startDate">
					</mt-datetime-picker>
				</div>
				<div v-else>
					<div v-show="heightShow">
						<div class="ti1">
						<img :src="src2" alt="" style="width:60%">
					</div>
					<p style="font-size:16px;color:#999;line-height: 1.7;">选择你的身高</p>
					<div style="padding: 0 10%;position: relative;">
						<mt-range style="margin: 50px auto 10px auto;position: relative;" v-model="rangeValue" :min="140" :max="200">
							<div slot="start">140cm</div>
							<div slot="end">200cm</div>
						</mt-range>
						<span class="pointer-label">{{rangeValue}}cm</span>
					</div>
					<div style="width:90%; margin:-30px auto 0px auto">
						<input type="button" value="下一步" class="btn btn-box" style="margin:80px 20% 0px 20%" @click="enterResiter">
					</div>
					</div>
				</div>
				<div class="phone2" v-if="registerMobile">
					<div class="tit">
						<img :src="src2" alt="" style="width: 30%;">
						<p>输入您的手机号和密码<br>完成注册</p>
						<div class="sub2">
							<form action="" id="user">
								<input class="text username" type="text" placeholder="输入您的手机号" name="mobile" v-model="mobile">
								<input class="text pwd" type="text" placeholder="设定您的登录密码" name="passwd" v-model="passwd">
								<input class="btn" type="button" value="注册" @click="locallinks">
							</form>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import { Picker } from 'mint-ui';
	import { Range } from 'mint-ui';
	import { MessageBox } from 'mint-ui';
	import myaddress from '../../static/city.json'; 
	import mapDrag from './mapDrag';
	export default {
		name: 'person',
		components: {
			'mt-picker': Picker,
			'mt-range': Range,
			mapDrag,
			MessageBox
		},
		data() {
			return {
				pickerVisible: new Date(),
				value: '',
				startDate: new Date('1970-01-01'),
				isshow: true,
				isnext: false,
				cityShow: false,
				dateShow: false,
				dateModal: true,
				rangeValue: 165,
				registerMobile:false,
				heightShow:true,
				mobile:'',
				passwd:'',
				src: '',
				src2: '',
				arr: [],
				select: "",
				dragData: {
					lng: null,
					lat: null,
					address: null,
					nearestJunction: null,
					nearestRoad: null,
					nearestPOI: null
				},
				imgs: [{
						url: 'http://m.hongniang.com/public/home/wap/images/re_woman.png'
					},
					{
						url: 'http://m.hongniang.com/public/home/wap/images/re_man.png'
					}
				],
				avaList: [{
						url: 'http://m.hongniang.com/public/home/wap/images/lo_woman.png',
						id: 1,
						text: '女神',
						txt: 'Woman'
					},
					{
						url: 'http://m.hongniang.com/public/home/wap/images/lo_man.png',
						id: 2,
						text: '男神',
						txt: 'Man'
					}
				],
				myAddressSlots: [{
						flex: 1,
						defaultIndex: 1,
						values: Object.keys(myaddress), //省份数组
						className: 'slot1',
						textAlign: 'center'
					}, {
						divider: true,
						content: '-',
						className: 'slot2'
					}, {
						flex: 1,
						values: [],
						className: 'slot3',
						textAlign: 'center'
					},
					{
						divider: true,
						content: '-',
						className: 'slot4'
					},
					{
						flex: 1,
						values: [],
						className: 'slot5',
						textAlign: 'center'
					}
				],
				myAddressProvince: '省',
				myAddressCity: '市',
				myAddresscounty: '区/县',
			}
		},
		methods: {
			handleConfirm(id) {
				let a = this.pickerVisible;
				this.dateModal = false;
				var resDate = a.getFullYear() + '-' + (a.getMonth() + 1) + '-' + a.getDate();
				this.src2 = this.imgs[id].url;
			},
			enterDate: function() {
				this.dateShow = true;
				this.isshow = false;
				this.isnext = false;
				this.src = this.arr[0].url;
				this.handleConfirm(this.arr[0].id - 1);
			},
			enterResiter(){
				this.registerMobile=true;
				this.dateModal=false;
				this.heightShow=false;
			},
			locallinks(){
				if(this.mobile!=''&&this.passwd!=''){
					MessageBox.alert('注册成功');
				}else{
					MessageBox.alert('请输入正确的手机号', '提示');
					console.log(this.arr[0].url+this.select+this.rangeValue+this.mobile+this.passwd)
				}
			},
			showModal: function(isbool, item) {
				this.isnext = isbool;
				this.isshow = false;
				this.arr.push(item);
			},
			bottomCity: function() {
				this.cityShow = true;
			},
			ok: function() {
//				console.log(this.select)
				this.cityShow = false;
			},
			cancle: function() {
				this.cityShow = false;
			},
			dragMap(data) {
//				console.log(data)
				this.dragData = {
					lng: data.position.lng,
					lat: data.position.lat,
					address: data.address,
					nearestJunction: data.nearestJunction,
					nearestRoad: data.nearestRoad,
					nearestPOI: data.nearestPOI
				}
			},
			onMyAddressChange(picker, values) {
				if(myaddress[values[0]]) {
					picker.setSlotValues(1, Object.keys(myaddress[values[0]]));
					picker.setSlotValues(2, myaddress[values[0]][values[1]]);
					this.myAddressProvince = values[0];
					this.myAddressCity = values[1];
					this.myAddresscounty = values[2];
					this.select = this.myAddressProvince + ' ' + this.myAddressCity + ' ' + this.myAddresscounty;
				}
			},
		},
		filters: { //时间转换
			formatDate(time) {
				var date = new Date(time);
				return formatDate(date, 'yyyy-MM-dd');
			}
		},
		beforeCreate: function() {
			document.getElementsByTagName("body")[0].className = "active";
		},
		beforeDestroy: function() {
			document.body.removeAttribute("class", "active");
		},
		mounted() {
			this.$nextTick(() => {
				this.myAddressSlots[0].defaultIndex = 0
			});
			this.ok();
//			console.log(this.rangeValue)
		}
	}
</script>
<style scoped>
	.register_sex {
		color: #999;
	}
	
	.register_sex .sub .tit {
		padding-top: 68px;
		color: #999;
		font-size: 28px;
		text-align: center;
		margin-bottom: 60px;
	}
	
	.register_sex .sub img {
		width: 35%;
	}
	
	.register_sex .sub .ti1 {
		color: #333;
		font-size: 32px;
	}
	
	.loc_ti {
		text-align: center;
		padding-top: 68px;
		margin-bottom: 40px;
	}
	
	.register_sex .btn {
		color: #999;
		background: #eee;
		border-radius: 40px;
		width: 60%;
		margin: 80px 20%;
		text-indent: 0px;
	}
	
	.register_sex input {
		width: 90%;
		height: 80px;
		font-size: 36px;
		border: 1px solid #ccc;
		border-radius: 5px;
		margin: 40px 5% 0 5%;
		text-indent: 20px;
	}
	
	.gearArea {
		font-family: Helvetica Neue, Helvetica, Arial, sans-serif;
		font-size: 20px;
		background-color: rgba(0, 0, 0, 0.2);
		display: block;
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		z-index: 9900;
		overflow: hidden;
		-webkit-animation-fill-mode: both;
		animation-fill-mode: both;
	}
	
	.picker,
	.area_btn_box {
		-webkit-animation: slideInUp .3s;
		animation: slideInUp .3s;
		vertical-align: middle;
		background-color: #d5d8df;
		color: #000;
		margin: 0;
		height: 360px;
		width: 100%;
		position: absolute;
		left: 0;
		bottom: 0;
		z-index: 9901;
		overflow: hidden;
		-webkit-transform: translate3d(0, 0, 0);
		transform: translate3d(0, 0, 0);
	}
	
	.gearArea .area_btn_box {
		position: absolute;
		left: 0;
		bottom: 360px;
		height: auto;
		z-index: 9901;
	}
	
	.area_btn_box {
		display: -webkit-box;
		display: -webkit-flex;
		display: -ms-flexbox;
		display: flex;
		-webkit-box-pack: justify;
		-webkit-justify-content: space-between;
		-ms-flex-pack: justify;
		justify-content: space-between;
		-webkit-box-align: stretch;
		-webkit-align-items: stretch;
		-ms-flex-align: stretch;
		align-items: stretch;
		background-color: #f1f2f4;
		position: relative;
	}
	
	.area_btn {
		color: #0575f2;
		font-size: 32px;
		line-height: 90px;
		text-align: center;
		padding: 0 20px;
	}
	
	.area_btn_box:before,
	.area_btn_box:after {
		content: '';
		position: absolute;
		height: 1px;
		width: 100%;
		display: block;
		background-color: #96979b;
		z-index: 15;
		-webkit-transform: scaleY(0.33);
		transform: scaleY(0.33);
	}
	
	.area_btn_box:before {
		left: 0;
		top: 0;
		-webkit-transform-origin: 50% 20%;
		transform-origin: 50% 20%;
	}
	
	.area_btn_box:after {
		left: 0;
		bottom: 0;
		-webkit-transform-origin: 50% 70%;
		transform-origin: 50% 70%;
	}
	
	.map {
		min-width: 300px;
		min-height: 300px;
		position: relative;
	}
	
	#js-container {
		height: 380px;
		width: 90%;
		margin: 0 5%;
		border-radius: 40px;
	}
</style>