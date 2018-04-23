<template>
	<div>
		<div class="register_sex">
			<div class="sub" v-show="isshow ? true:false">
				<div class="tit"> 您是男神还是女神？</div>
				<div @click="showModal(true)">
					<a href="javascript:;">
						<img src="http://m.hongniang.com/public/home/wap/images/lo_woman.png" alt="">
					</a>
					<p class="ti1">女神</p>
					<p>Woman</p>
				</div>
				<div style="margin-top: 20px;" @click="showModal(true)">
					<a href="javascript:;">
						<img src="http://m.hongniang.com/public/home/wap/images/lo_man.png" alt="">
					</a>
					<p class="ti1">男神</p>
					<p>Man</p>
				</div>
			</div>
			<div v-show="isnext">
				<div class="loc_ti">以下是您所在位置，点击位置区域<br>进行修改</div>
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
					<input class="btn" type="submit" value="下一步">
				</form>
			</div>
		</div>
	</div>
</template>

<script>
	import { Picker } from 'mint-ui';
	import myaddress from '../../static/city.json'; 
	export default {
		name: 'person',
		components:{
			'mt-picker': Picker
		},
		data() {
			return {
				isshow:true,
				isnext:false,
				cityShow:false,
				select:"",
				myAddressSlots: [
		          {
		            flex: 1,
		            defaultIndex: 1,    
		            values: Object.keys(myaddress),  //省份数组
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
		        myAddressProvince:'省',
		        myAddressCity:'市',
		        myAddresscounty:'区/县',
			}
		},
		methods: {
			showModal: function(isbool){
				this.isnext=isbool;
				this.isshow=false;
			},
			bottomCity:function(){
				this.cityShow=true;
			},
			ok:function(){
				console.log(this.select)
				this.cityShow=false;
			},
			cancle:function(){
				this.cityShow=false;
			},
			onMyAddressChange(picker, values) {
		       if(myaddress[values[0]]){
		          picker.setSlotValues(1,Object.keys(myaddress[values[0]])); 
		          picker.setSlotValues(2,myaddress[values[0]][values[1]]); 
		          this.myAddressProvince = values[0];
		          this.myAddressCity = values[1];
		          this.myAddresscounty = values[2];
		          this.select=this.myAddressProvince+' '+this.myAddressCity+' '+this.myAddresscounty;
		        }
	      	},
		},
		beforeCreate: function() {
	        document.getElementsByTagName("body")[0].className="active";
	    },
	    beforeDestroy: function() {
	        document.body.removeAttribute("class","active");
	    },
	    mounted(){
	      this.$nextTick(() => { 
	        this.myAddressSlots[0].defaultIndex = 0    
	      });
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
.loc_ti{
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
.register_sex input{
	width: 90%;
	height: 80px;
	font-size: 36px;
    border: 1px solid #ccc;
    border-radius: 5px;
    margin: 40px 5% 0 5%;
    text-indent: 20px;
}
.gearArea{
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
.picker,.area_btn_box{
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
.gearArea .area_btn_box{
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
.area_btn_box:before, .area_btn_box:after {
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
</style>