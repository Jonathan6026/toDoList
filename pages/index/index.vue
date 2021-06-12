<template>
	<view class="content">
		<view class="header">
			<view class="headerLeft">
				<text>列表</text>
				<text>10条</text>
			</view>
			<view class="headerRight">
				<view class="headerRightList activateStatus">All</view>
				<view class="headerRightList">ToDo</view>
				<view class="headerRightList">Finish</view>
			</view>
		</view>
		<view class="list">
			<view class="listItem">
				<view class="listBox">
					<view class="checkBox">
						
					</view>
				</view>
				<view class="listText">
					第一件事情吃饭
				</view>
			</view>
		</view>
		<view class="list listItemDone">
			<view class="listItem">
				<view class="listBox">
					<view class="checkBox">
						
					</view>
				</view>
				<view class="listText">
					第一件事情吃饭
				</view>
			</view>
		</view>
		<view class="bottom">
			<view class="createComponent">
				<text class="iconfont iconjia"></text>
			</view>
			<view class="createList">
				<view class="createInput">
					<input type="text" placeholder="请输入创建内容"/>
				</view>
				<view class="createButton">创建</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		onLoad() {

		},
		methods: {

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
.headerRight .headerRightList {

	
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
</style>
