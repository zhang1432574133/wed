<template>
	<div class="wsnav">
		<router-view />
		<ul>
			<li :class="{ 'is-selected':index==selected }" v-for="(item,index) in tabs" @click="handleChange(index)">
				<a href="javascript:;">
					<i class="iconfont" :class="item.class"></i>
					<p>{{item.tabName}}</p>
				</a>
			</li>
		</ul>
	</div>
</template>
<script>
export default {
  name: 'bottom',
  data () {
    return {
    	selected:0,
    	tabs:[
    		{ name:'', class:'icon-home',tabName:'首页'},
    		{ name:'person', class:'icon-geren',tabName:'个人'}
    	],
    }
  },
  methods: {
  	handleChange(index){
		this.selected=index;
		const nav = this.tabs[index];
		this.$router.push("/" + nav.name)
	},
  },
  mounted: function(){
  	var index=0;
  	switch (this.$route.path) {
        case "/person":
  			index=1;
            break;
        default:
          index=0;
          break;
  	}
  	this.handleChange(index)
  }
}
</script>
