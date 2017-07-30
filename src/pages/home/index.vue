<style lang="less" scoped>

</style>
<template>
	<div>
		<v-header title="首页">
			<router-link slot="left" to="/">首页</router-link>
			<router-link slot="right" to="/signout">退出</router-link>
		</v-header>
		<div style="padding: 50px;text-align: center;">{{user.name}}欢迎回家</div>
		<v-footer>
			<li>何如月</li>
			<li>月月</li>
		</v-footer>
	</div>
	
</template>
<script>
import {mapActions, mapState } from 'vuex'
import { CART_LIST,CART_TIST } from 'store/cart'
import {getShopId} from '../common/js/getShopIp'

export default {
	data() {
		return {
			
		}
	},
	computed: {
		...mapState({ user: state => state.user ,cart: state => state.cart}),
	},
	created() {
		var $this = this;
		$this.init(function(){
			var arr = getShopId($this.cart)
			$this.arrList(arr);
		});
	},
	methods: {
		...mapActions([ CART_LIST,CART_TIST ]),
		init(callback) {
			this.axios.get(confing.api.orderList).then((response) => {
				console.log(response.data)
				if(response.data.code === 200){
					this.CART_LIST({
						totalPage:20,
						nums:10
					})
					
				}
				typeof callback == 'function' && callback()//执行完上面的函数之后执行回调的函数
			})
			
		},
		arrList(arr){
			this.CART_TIST({
				log:arr.log,
				lom:arr.lom
			})
		}
	}


}
</script>