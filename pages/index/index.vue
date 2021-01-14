<template>
	<view>
		<view class="cf-hengSpace-B itemBox" style="margin-top: 40upx;">只能选一项，第1种：</view>
		<view class="cf-hengSpace-B itemBox" v-for="(item, index) in list" :key="index">
			<view>{{item.name}}</view>
			<ayswitchR :themeColor="themeColor" :isGroup="true" :index="index" :item="item" :switch="item.switch" @change="switchFun_Group" ></ayswitchR>
		</view>
		
		
		<view class="cf-hengSpace-B itemBox" style="margin-top: 40upx;">只能选一项，第2种：</view>
		
		<view class="cf-hengSpace-B itemBox"  v-for="(item, index) in list" :key="'2'+index">
			<view>{{item.name}}</view>
			<ayswitch :themeColor="themeColor" :isGroup="true" :index="index" :item="item" :switch="item.switch" @change="switchFun_Group"  ></ayswitch>
		</view>
		
		
		<view class="cf-hengSpace-B itemBox" style="margin-top: 40upx;">不关联选，第1种：</view>
		
		<view class="cf-hengSpace-B itemBox"  v-for="(item, index) in list2" :key="'3'+index">
			<view>{{item.name}}</view>
			<ayswitchR :themeColor="themeColor" :index="index" :item="item" :switch="item.switch" @change="switchFun" ></ayswitchR>
		</view>
		
		
		
		<view class="cf-hengSpace-B itemBox" style="margin-top: 40upx;">不关联选，第2种：</view>
		
		<view class="cf-hengSpace-B itemBox"  v-for="(item, index) in list2" :key="'4'+index">
			<view>{{item.name}}</view>
			<ayswitch :themeColor="themeColor" :index="index" :item="item" :switch="item.switch" @change="switchFun" ></ayswitch>
		</view>
		
	</view>
</template>

<script>
	import ayswitchR from '@/components/ay-switch/ay-switch-round.vue'
	import ayswitch from '@/components/ay-switch/ay-switch.vue'
	export default {
		components: {
			ayswitchR,
			ayswitch
		},
		data() {
			return {
				themeColor:'#33CCCC',
				val:'',
				list:[{
					name:'选项1',
					val:'1',
					switch:true,
				},
				{
					name:'选项2',
					val:'2',
					switch:false,
				},
				{
					name:'选项3',
					val:'3',
					switch:false,
				}],
				list2:[{
					name:'选项1',
					val:'1',
					switch:true,
				},
				{
					name:'选项2',
					val:'2',
					switch:false,
				},
				{
					name:'选项3',
					val:'3',
					switch:false,
				}],
				
			}
		},

		onLoad() {
			let that = this;
			
		},
		methods: {
			switchFun_Group(e){
				let that = this;
				that.val = e.item.val ;
				that.list.forEach(item=>{
					let index = that.list.indexOf(item) ;
					if(index!==e.index){
						item.switch = false ;
					}else{
						item.switch = true ;
					}
				})
			},
			
			async switchFun(e) {
				let that = this;
				let item = e.item;
				let index = e.index;
				let isSwitch = item.switch;//false 已挂起 true 开通的
				
				let tip = '' ;
				if(isSwitch){
					tip = '确认关闭吗？';
				}else{
					tip = '确认开启吗？';
				}
				uni.showModal({
					title: '提醒',
					content:  tip ,
					success(res) {
						if (res.confirm) {
							if(isSwitch){
								
							}else{
								
							}
							that.list2[index].switch = !isSwitch;
							
						} else if (res.cancel) {
							
						}
					}
				})
				
			},
		}

	}
</script>

<style lang="scss">
	.cf-hengSpace-B {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		width: 100%;
	}
	
	.itemBox{
		width: 80%;
		margin: 10upx 60upx;
	}
	
</style>
