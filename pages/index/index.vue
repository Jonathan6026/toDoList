<template>
	<view class="content">
		<!-- 头部菜单 -->
		<view class="header" v-if="list.length !== 0">
			<view class="headerLeft">
				<text>列表</text>
				<text>10条</text>
			</view>
			<view class="headerRight">
				<view class="headerRightList" 
					  :class="{'activateStatus':tabStatus===1}"
					  @click="switchTab(1)">
					All
				</view>
				<view class="headerRightList" 
					  :class="{'activateStatus':tabStatus===2}"
					  @click="switchTab(2)">
					ToDo
				</view>
				<view class="headerRightList" 
					  :class="{'activateStatus':tabStatus===3}"
					  @click="switchTab(3)">
					Finish
				</view>
			</view>
		</view>
		<!-- 缺省样式 -->
		<view class="noneItem" v-if="list.length === 0">
			<image class="noneImage" src="../../static/default.png" mode="aspectFill"></image>
			<view class="noneText">当前任务列表为空噢！</view>
		</view>
		
		<!-- 任务样式  listItemDone-->
		<view 
			class="list" 
			:class="{'listItemDone':item.status}"
			v-for="(item,index) in dataList" :key = "index"
		>
			<view class="listItem">
				<view class="listBox">
					<view class="checkBox" 	@click="finish(item.id)">
						
					</view>
				</view>
				<view class="listText">
					{{item.content}}
				</view>
			</view>
		</view>
		
		<!-- 创建组件 -->
		<view class="bottom">
			<!-- 创建按钮 -->
			<view class="createComponent" @click="createItem" >
				<text class="iconfont iconjia"></text>
			</view>
			<!-- 创建输入 -->
			<view class="createList" v-if="activate" :focus="focusInput">
				<view class="createInput">
					<input 
						type="text" placeholder="请输入创建内容"
						v-model="value" 
					/>
					<!-- 双向绑定输入值-->
				</view>
				<view class="createButton" @click="addItem">创建</view>
			</view>
		</view>
		
		<!-- 透明背景 -->
		<view class="shdow" v-if="shdow" @click="shdowHide">
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list:[
					// {
					// 	content:"11111"
					// },
					// {
					// 	content:"22222"
					// }
				],
				value:"",
				activate:false,
				shdow:false,
				focusInput:false,
				tabStatus:1
			}
		},
		onLoad() {

		},
		computed: {
			dataList() {
				let list = JSON.parse(JSON.stringify(this.list))
				let newList = []
				
				/* All的时候 */
				if (this.tabStatus === 1) {
					return list
				}
				/* ToDo的时候 */
				if (this.tabStatus === 2) {
					list.forEach((item)=> {
						/* 如果状态是false就返回 */
						if (!item.status) {
							newList.push(item)
						}
					})
					return newList
				}
				/* Finish的时候 */
				if (this.tabStatus === 3) {
					list.forEach((item)=> {
						/* 如果状态是false就返回 */
						if (item.status) {
							newList.push(item)
						}
					})
					return newList
				}
			}
		},
		methods: {
			/* 打开创建输入 */
			createItem() {
				this.activate = !this.activate
				this.shdow = !this.shdow
				this.focusInput = true
				console.log(this.activate)
			},
			/* 阴影show */
			shdowShow() {
				setTimeout(()=>{
					this.shdow = true
				},100) 
			},
			/* 阴影hide */
			shdowHide() {
				setTimeout(()=> {
					this.shdow = false
					this.activate = !this.activate
				},10)
			},
			/* 创建List */
			addItem() {
				if (this.value !== "") {
					this.list.push({
						/* 以时间戳为ID */
						id:new Date().getTime(),
						content:this.value,
						status:false
					})
					this.value = ""
					this.shdowHide()
				} 
				else {
					/* 弹出提示框 */
					uni.showToast({
						title:"请输入内容",
						icon:'none'
					})
				}

			},
			/* 完成Item */
			finish(id) {
				let index = this.list.findIndex((item)=> item.id === id)
				this.list[index].status = !this.list[index].status
			},
			switchTab(i) {
				this.tabStatus = i
			}
		}
	}
</script>

<style>
@import "../../common/icon.css";
/* .content {
	height: 100vh;
	background:linear-gradient(#99f,#f99);
}	 */
	
.header {
	height: 70px;
	text-align: 40px;
	display: flex;
	justify-content: space-between;
	align-items: center; //垂直居中
	font-size: 15px;
	box-shadow: -1px 1px 5px 1px rgba(0,0,0,0.1);
}
.headerLeft {
	/* width: 100%; */
	flex-grow: 1;
}
.headerLeft text {
	margin: 0 6px;

}
.headerRight {
	display: flex;
	background:linear-gradient(#99f,#f99);
	height: 50px;
	width: 200px;
	text-align: 50px;
	border-radius: 8px;
	box-shadow: 0 2px 3px 0 rgba(0,0,0,.1);
	align-items: center; //垂直居中
	justify-content: space-around;
	overflow: hidden;
}
.activateStatus {
	color: #007AFF;
}
.list {
	position: relative;
	
}
.listItem {
	position: relative;
	display: flex;
	align-items: center;
	margin: 15px;
	padding: 15px;
	color: #0c3854;
	background-color: #cfebfd;
	border-radius: 15px;
	box-shadow: -1px 1px 5px 1px rgba(0,0,0,0.1);
}
.listBox {
	padding-right: 15px;
}
.checkBox {
	width: 20px;
	height: 20px;
	border-radius: 50%;
	background: #FFFFFF;
	box-shadow: 0 0 5px 1px rgba(0,0,0,.1);
}

.listItemDone .checkBox {
	position: relative;
	background-color: #eee;
}
.listItemDone .checkBox::after {
	content: "";
	position: absolute;
	width: 10px;
	height: 10px;
	top: 0;
	bottom: 0;
	left: 0;
	right: 0;
	margin: auto;
	border-radius: 50%;
	background-color: #CFEBFD;
	box-shadow: 0 0 2px 0px rgba(0,0,0,0.2) inset;
}
.listItemDone .listText {
	color: #999999;
}
.listItemDone .listItem:after {
	content: "";
	position: absolute;
	top: 0;
	bottom: 0;
	right: 10px;
	left: 40px;
	height: 2px;
	margin: auto 0;
	background-color: #bdcdd8;
}
.createComponent {
	display: flex;
	justify-content: center; //左右居中
	align-items: center;     //垂直居中
	position: fixed;
	bottom: 20px;
	left: 0;
	right: 0;
	margin: 0 auto;
	width: 75rpx;
	height: 75rpx;
	border-radius: 50%;
	background-color: #deeff5;
}
.createList {
	display: flex;
	align-items: center;
	position: fixed;
	bottom: 80px;
	left: 60px;
	padding: 0 0 0 15px;
	border-radius: 50px;
	background-color: #fff;
	box-shadow: -1px 1px 5px 2px rgba(0,0,0,0.1),-1px 1px 1px 0 rgba(255,255,255) inset;
	z-index: 2;
}
.createButton {
	display: flex;
	align-items: center;
	justify-content: center;
	flex-shrink: 0;
	width: 80px;
	height: 50px;
	border-radius: 50px;
	font-size: 16px;
	color: #88d4ec;
	background-color: #ffffff;
	box-shadow: -2px 0px 2px 1px rgba(0,0,0,0.1);

}
.createList:after {
	content: "";
	position: absolute;
	right: 15px;
	left: 0;
	bottom: -10px;
	margin: 0 auto;
	height: 20px;
	width: 20px;
	transform: rotate(45deg);
	box-shadow: 1px 2px 5px 2px rgba(0,0,0,0.1);
	background-color: #fff;
	
}

.noneItem {
	padding-top: 150px;
}
.noneImage {
	display: flex;
	justify-content: center;
	width: 100%;
}
.noneText {
	text-align: center;
	color: #ccc;
	font-size: 14px;
}

/* 阴影部分 */
.shdow {
	position: fixed;
	top: 0;
	right: 0;
	left: 0;
	bottom: 0;
	background: rgba(0,0,0,.5);
}
</style>
