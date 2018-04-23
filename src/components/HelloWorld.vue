<template>
	<div class="main">
		<div class="w-wapper">
			<div class="swiper-container">
        <div class="swiper-wrapper">
            <div class="swiper-slide" v-for="str in bannerImg" :style="{background: 'url('+str.url+')'}">
            	<router-link to="/home"></router-link>
            </div>
        </div>
        <div class="swiper-pagination swiper-pagination-white"></div>
    	</div>
	  </div>
	  <nav class="nav-wrap swiper-container1">
			<ul class="nav-list swiper-wrapper">
				<li class="nav-list-item swiper-slide" v-for="item in navList" :key="item.id"> 
					<a href="javascript:;">
						<img src="http://m.hongniang.com/public/home/wap/images/mhongniang001.png" alt="">{{item.text}}
					</a>
				</li>
			</ul>
		</nav>
		<div class="WStj">
			<div class="tjlist">
				<p class="p1">推荐会员<a href=""></a></p>
				<ul>
					<li>
						<a href="">
							<img src="http://m.hongniang.com/data/upload/photo/2015-01-30/290278_1422582315.png" alt="">
						</a>
						<p>回眸一睹相思梦</p>
						<p><span>26岁</span><span>浙江杭州</span></p>
					</li>
					<li>
						<a href="">
							<img src="http://m.hongniang.com/data/upload/photo/2015-01-30/290278_1422582315.png" alt="">
						</a>
						<p>回眸一睹相思梦</p>
						<p><span>26岁</span><span>浙江杭州</span></p>
					</li>
					<li>
						<a href="">
							<img src="http://m.hongniang.com/data/upload/photo/2015-01-30/290278_1422582315.png" alt="">
						</a>
						<p>回眸一睹相思梦</p>
						<p><span>26岁</span><span>浙江杭州</span></p>
					</li>
					<li>
						<a href="">
							<img src="http://m.hongniang.com/data/upload/photo/2015-01-30/290278_1422582315.png" alt="">
						</a>
						<p>回眸一睹相思梦</p>
						<p><span>26岁</span><span>浙江杭州</span></p>
					</li>
					<li>
						<a href="">
							<img src="http://m.hongniang.com/data/upload/photo/2015-01-30/290278_1422582315.png" alt="">
						</a>
						<p>回眸一睹相思梦</p>
						<p><span>26岁</span><span>浙江杭州</span></p>
					</li>
				</ul>
			</div>
		</div>
		<div class="hltxt"> 
			<p class="p1 xuetang">
				<a href="javascript:void(0)">婚恋学堂</a>
			</p> 
				<a href="javascript:;"> 
					<img src="http://www.hongniang.com/public/images/default2.jpg" alt=""> </a> 
		</div>
		<div class="hltxt"> 
			<p class="p1 xuetang">
				<a href="javascript:void(0)">恋爱交友</a>
			</p> 
				<a href="javascript:;"> 
					<img src="http://www.hongniang.com/public/home/wap/images/jiaoyouquan.jpg" alt=""> </a> 
		</div>
		<Bottom></Bottom>
	</div>
</template>

<script>
import Bottom from '../components/footer.vue';
import Swiper from 'swiper';
import 'swiper/dist/css/swiper.min.css';
export default {
  name: 'HelloWorld',
  components:{Bottom},
  data () {
    return {
    	bannerImg:[
    		{url:'http://m.hongniang.com/data/upload/event/20180416/5ad44fac9a83b.jpg'},
    		{url:'http://m.hongniang.com/data/upload/event/20180416/5ad44fac9a83b.jpg'}
    	],
    	navList:[
    		{text:'导航',id:1},
    		{text:'服务员',id:2},
    		{text:'导航',id:3},
    		{text:'服务员',id:4},
    		{text:'导航',id:5},
    		{text:'服务员',id:6}
    	]
    }
  },
  methods:{
  	mySwiper: function(name,circleName,obj){
  		var swiper = new Swiper(name, obj);
  	}
  },
  mounted: function(){
  	this.mySwiper('.swiper-container1','.swiper-pagination',{
  		freeMode : true,
		  slidesPerView : 'auto',
		  freeModeSticky : true ,		 
		  freeModeMomentumBounce : false,		
  	});
  	this.mySwiper('.swiper-container','.swiper-pagination',{
  		loop: true,
			pagination: {
      	el: '.swiper-pagination',
    	},
    	autoplay:true,	
  	});
  }
  
  
}
</script>
