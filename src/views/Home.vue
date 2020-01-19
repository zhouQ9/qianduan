<template>
	<div class="body">
		<div class="banner">
			<ul>
				<li>
					<router-link to="/recommoned" class="router"><p class="text">推荐</p></router-link>
				</li>
				<li>
					<router-link to="/follow" class="router"><p class="text">关注</p></router-link>
				</li>
				<li>
					<router-link to="/hot" class="router"><p class="text">热榜</p></router-link>
				</li>
			</ul>
		</div>
		<div class="container">
			<div class="row" v-for="(item, index) in recommoned" :key="index">
				<div class="col-4"><img :src="item.banner" alt="" /></div>
				<div class="col-8">
					<h3 class="title-text">{{ item.title }}</h3>
				<div class="introduction-box">
					<p class="introduction-text">{{ item.introduction }}...阅读全文</p>
				</div>
				<p class="meta">{{ item.updated }} 更新，{{ item.viewCount }}次浏览</p>
				<span v-for="(section, index) in item.sections" :key="index" class="section">{{ section.sectionTitle }}</span>
			</div>
			
			</div>
		</div>
	</div>
</template>
<script>
export default {
	name: 'recommoned',
	// data 一定要是个函数
	data() {
		return {
			recommoned: []
		};
	},
	created() {
		this.axios.get('http://localhost:8080/api/special').then(res => {
			console.log(res);
			console.log('ceece');
			this.recommoned = res.data.data;
		});
	}
};
</script>
<style lang="scss" scoped>
.body {
	background-color: #f6f6f6;
}
ul {
	list-style-type: none;
}
li {
	font-size: larger;
	margin-top: 10px;
	margin-left: 50px;
	float: left;
}
.title-text {
	color: #000000;
	font-size: 22px;
	margin-left: -240px;
	
}
.introduction-text {
	font-size: 18px;
	margin-top: -0.625rem;
	height: 300px;
}
.introduction-box {
	height: 7.8125rem;
	margin-left: -1.25rem;
}
.meta {
	font-size: 19px;
	margin-top: -0.625rem;
	margin-top: 50px;
	color: #333333;
	margin-left: -9.375rem;
}
.banner {
	margin-top: 70px;
	height: 60px;
	width: 60%;
	margin-left: 225px;
	border: 1px solid #d6d6d6;
	box-shadow: 2px 5px 5px #ddd;
	display: flex;
	align-items: center;
	background-color: #ffffff;
}
h1 {
	color: #0084ff;
}
.text {
	color: #000000;
	font-size: 15px;
}
.router {
	text-decoration: none;
}
.container {
	overflow: auto;
	margin: 0 auto;
	width: 60%;
	margin-left: 225px;
	background-color: #ffffff;
	font-size: 25px;
	.row {
		background-color: #ffffff;
		display: flex;
		border: 1px solid #d6d6d6;
		border-radius: 4px;
		padding: 14px;
		box-shadow: 0 1px 3px 0 rgba(26, 26, 26, 0.1);
		.col-4 {
			flex: 0 0 33%;
			height: auto;
			img {
				margin-top: 60px;
				width: 14.0625rem;
				height: 7.8125rem;
				border-radius: 10px;
				margin-left: 1.875rem;
			}
		}
	}
}
</style>
