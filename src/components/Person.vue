<template>
	<div>
		{{msg}}
		<Bottom></Bottom>
	</div>
</template>

<script>
import Bottom from '../components/footer.vue';
export default {
  name: 'person',
  components:{Bottom},
  data () {
    return {
    	msg:"这是个人页面"
    }
  },
  methods: {
  },
}
</script>
