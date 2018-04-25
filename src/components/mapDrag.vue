<template>
	<div id="js-container" class="map"></div>
</template>

<script>
import remoteLoad from '@/utils/remoteLoad.js'
export default{
	props:['lat','lng'],
	data () {
		return{
			AMapUI: null,
      		AMap: null
		}
	},
	methods: {
		initMap () {
			let AMapUI=this.AMapUI=window.AMapUI
		let AMap=this.AMap=window.AMap
		  AMapUI.loadUI(['misc/PositionPicker'], PositionPicker => {
		    let mapConfig = {
		      zoom: 16,
		      cityName: '上海'
		    }
		    if (this.lat && this.lng) {
		      mapConfig.center = [this.lng, this.lat]
		    }
		    let map = new AMap.Map('js-container', mapConfig)
		    // 创建地图拖拽
		    let positionPicker = new PositionPicker({
		      mode: 'dragMap', // 设定为拖拽地图模式，可选'dragMap'、'dragMarker'，默认为'dragMap'
		      map: map // 依赖地图对象
		    })
		    // 拖拽完成发送自定义 drag 事件
		    positionPicker.on('success', positionResult => {
		      // 过滤掉初始化地图后的第一次默认拖放
		      if (!this.dragStatus) {
		        this.dragStatus = true
		      } else {
		        this.$emit('drag', positionResult)
		      }
		    })
		    // 启动拖放
		    positionPicker.start()
		  })
		}
	},
	async created () {
		if (window.AMap && window.AMapUI){
			this.initMap()
		}else{
			await remoteLoad(`http://webapi.amap.com/maps?v=1.3&key=6a30e481a301aa3148e426af038e87c2`)
			await remoteLoad('http://webapi.amap.com/ui/1.0/main.js')
			this.initMap()
		}
	}
	
}
</script>

<style>
</style>