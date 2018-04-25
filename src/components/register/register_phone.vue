<template>
	<div class="phone2">
		<div class="tit">
			<img :src="src3" alt="" style="width: 30%;">
			<p>输入您的手机号和密码<br>完成注册</p>
			<div class="sub2">
				<form action="" id="user">
					<input class="text username" type="text" placeholder="输入您的手机号" value="" name="mobile">
					<input class="text pwd" type="text" placeholder="设定您的登录密码" value="" name="passwd">
					<input class="btn" type="button" value="注册">
				</form>
			</div>
		</div>
	</div>
</template>
<script>
	export default {
		name: 'mobile',
		data() {
			return {
				src2: '',
				imgs: [{
						url: 'http://m.hongniang.com/public/home/wap/images/re_woman.png'
					},
					{
						url: 'http://m.hongniang.com/public/home/wap/images/re_man.png'
					}
				],
			}
		},
		methods: {
			
		},
		 mounted: function(){
		 }
	}
</script>

<style>

</style>