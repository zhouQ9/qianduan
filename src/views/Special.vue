<template>
	<div>
		<div class="banner">
			<h3 style="margin-left: 240px;">全部专题</h3>
			<h4 style="margin-left: 20px;margin-top: 2px;">共有{{ specials.length }}个文章</h4>
		</div>
		<div class="container">
			<div class="row" v-for="(item, index) in specials" :key="index">
				<div class="col-4"><img :src="item.banner" /></div>
				<div class="col-8">
					<h4 class="title-color">{{ item.title }}</h4>
					<div class="">
						<button class="button"><h4 style="color: #1E90FF;font-size: 1.125rem;font-weight: bold;">关注专题</h4></button>
					</div>
					<p class="meta">{{ item.updated }} 更新,{{ item.viewCount }}次浏览</p>

					<p class="introduction">{{ item.introduction }}</p>
					<span v-for="(section, index) in item.sections" :key="index" class="section">{{ section.sectionTitle }}</span>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'special',
	data() {
		return {
			specials: [],
			page:0 ,
			onFetching: false,
			scroll: ''
		};
	},
	created() {
		
		// this.$nextTick(function() {
		// 	this.box = this.$refs.viewBox;
		// 	this.box.addEventListener(
		// 		'scroll',
		// 		() => {
		// 			var scrollTop = tis.$refs.viewBox.scrollTop;
		// 			var scrollHeight = this.$refs.viewBox.scrollHeight;
		// 			var clientHeight = this.$refs.viewBox.clientHeight;
		// 			if (this.onFetching) {
		// 			} else {
		// 				if (clientHeight >= scrollHeight - scrollTop - 5) {
		// 					this.onFetching = true;
		// 					setTimeout(() => {
		// 						this.page += 1;
		// 						this.get();
		// 						this.onFetching = false;
		// 					}, 1000);
		// 				}
		// 			}
		// 		},
		// 		false
		// 	);
		// });
	},
	mounted() {
		this.get();
	},
	methods: {
		get() {
			this.axios
				.get('http://localhost:8080/api/special/all', {
					params: {
						catis_id: 1,
						page: this.page,
					}
				})
				.then(res => {
					console.log(res.data.data.length);
					this.specials = res.data.data;
					this.specials.length = res.data.data.length;
				});
		},
		scrollDs() {
			//变量scrollTop是滚动条滚动时，距离顶部的距离
			var scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
			//变量windowHeight是可视区的高度
			var windowHeight = document.documentElement.clientHeight || document.body.clientHeight;
			//变量scrollHeight是滚动条的总高度
			var scrollHeight = document.documentElement.scrollHeight || document.body.scrollHeight;
			//滚动条到底部的条件
			if (scrollTop + windowHeight == scrollHeight) {
				//到了这个就可以进行业务逻辑加载后台数据了
				this.loadMore();
			}
		},
		mounted() {
			window.addEventListener('scroll', this.scrollDs);
		}
	}
};
</script>

<style lang="scss" scoped>
h3 {
	color: #1a1a1a;
	font-size: 30px;
}
h4 {
	color: #a8b2b4;
	font-size: 20px;
}
.button{
	width: 6.25rem;
	border: none;
	background-color: rgb(235,245,255);
	color: rgb(30,134,255);
	height: 40px;
	border-radius: 5px;
	margin-left: 40.625rem;
	margin-top: -9.375rem;
	}
.title-color{
	color: black;
	font-size: 1.25rem;
	font-weight: bold;
}
.meta{
	margin-top: -0.625rem;
	color: gray;
}

.banner {
	margin-bottom: 10px;
	margin-top:70px;
	height: 100px;
	border: 1px solid #d6d6d6;
	box-shadow: 2px 5px 5px #ddd;
	padding-left: 10;
	display: flex;
	align-items: center;
	img {
		width: 12.5rem;
		height: 6.25rem;
	}
}
.container {
	overflow: auto;
	margin: 0 auto;
	width: 70%;
	.row {
		background-color: #ffffff;
		display: flex;
		border: 1px solid #d6d6d6;
		border-radius: 4px;
		height: auto;
		padding: 14px;
		box-shadow: 0 1px 3px 0 rgba(26, 26, 26, 0.1);
		.col-4 {
			flex: 0 0 33;
			height: auto;
			img {
				width: 21.875rem;
				height:9.375rem;
				border-radius: 10px;
			}
		}
		.col-8 {
			margin-left: 30px;
		}
	}
}
.introduction {
	font-size: 18px;
	// color: #5c5e5c;
	margin-top: 0.625rem;
}
</style>
