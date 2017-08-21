<template>
	<div class="tab1">
		<header class="head">
			<div class="headimg">
				<img src="../assets/ptimg.jpg">
				<button>未登录</button>
				<span>请点击登录</span>
			</div>
		</header>
		<div >
			<mt-cell title="菜单"></mt-cell>

			<mt-cell title="我的统计数据" is-link to=""> 
			     <img slot="icon" src="../assets/data.png" width="24" height="24">
			</mt-cell>

			<mt-cell title="未来计划表" is-link to=""> 
			     <img slot="icon" src="../assets/plan.png" width="24" height="24">
			</mt-cell>

			<mt-cell title="小憩" is-link to=""> 
			     <img slot="icon" src="../assets/sofa.png" width="24" height="24">
			</mt-cell>

			<mt-cell title="云同步" is-link to=""> 
			     <img slot="icon" src="../assets/云.png" width="24" height="24">
			</mt-cell>
		</div>
	</div>
</template>
<script>
export default{
	data(){
		return{
			
		}		
	},
	methods:{
		
	}
}

</script>

<style>
*{
	padding: 0;
	margin: 0
}
.head {
	width: 90%;
	height: 140px;
	padding-top: 12%;
	padding-left: 10%;
	background-image: url(../assets/bg.jpg);
}
.headimg{
	width: 25%;
	height: 50%;
	border-radius: 50px;
	background: red
}
.headimg img{
	width: 100%;
	height: 100%;
	border-radius: 50px;
}
.headimg button{
	border: none;
	background: none;
	font-size: 14px;
	margin: 10px
}
.headimg span{
	font-size: 12px;
	color: grey
}
.mint-cell-wrapper {
    font-size: 15px;
    text-align: left;
    font-weight: bold;
}
.mint-cell-text {
    margin-left: 10px;
}
</style>
