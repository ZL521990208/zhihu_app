<template>
	<div>
		<div class="zhuanlan-header">
					<div class="zhuanlan-header-content">
						<router-link to="/explore" class="zh-logo"><img src="../assets/image/知乎.png" height="30px"
							 width="80px" /></router-link>
						<div class="zhuanlan-write-btn">
							<div class="write-psgs">
								<img src="../assets/image/write-blue.png" width="20px" height="20px" />
								写文章
							</div>
							<div>
								<svg class="more" viewBox="0 0 24 24" width="24" height="24"><path d="M5 14a2 2 0 1 1 0-4 2 2 0 0 1 0 4zm7 0a2 2 0 1 1 0-4 2 2 0 0 1 0 4zm7 0a2 2 0 1 1 0-4 2 2 0 0 1 0 4z" fill-rule="evenodd"></path></svg></div>
						</div>
					</div>
				</div>

		<div class="container-top">
			<div class="top-img"><img src="../assets/image/logon.png" /></div>
			<h3>随心写作，自由表达</h3>
			<button class="top-button">开始写文章</button>
		</div>

		<div class="container">
			<div class="con-left"></div>
			<div class="con-home">
				<h5>申请开通专栏</h5>
				<h4>专栏·发现</h4>

				<div class="row">
					<div class="column" v-for="(item, index) in columns" :key="index">
						<img :src="item.imageUrl" onclick="location.href= 'https://zhuanlan.zhihu.com/jyzyx0'" />
						<h3 class="title">{{ item.title }}</h3>
						<h4 class="description">{{ item.description }}</h4>
						<h5 class="follower">{{ item.followers }}人关注|{{ item.articlesCount }}篇文章</h5>
						<button class="column-button">进入专栏</button>
					</div>
				</div>
				<button class="change-button" @click="loadMore">
					<svg class="Zi Zi--Refresh Button-zi" fill="currentColor" viewBox="0 0 24 24" width="1.2em" height="1.2em">
						<path
							d="M20 12.878C20 17.358 16.411 21 12 21s-8-3.643-8-8.122c0-4.044 3.032-7.51 6.954-8.038.034-1.185.012-1.049.012-1.049-.013-.728.461-1.003 1.057-.615l3.311 2.158c.598.39.596 1.026 0 1.418l-3.31 2.181c-.598.393-1.08.12-1.079-.606 0 0 .006-.606-.003-1.157-2.689.51-4.675 2.9-4.675 5.708 0 3.21 2.572 5.822 5.733 5.822 3.163 0 5.733-2.612 5.733-5.822 0-.633.51-1.148 1.134-1.148.625 0 1.133.515 1.133 1.148"
							fill-rule="evenodd"
						></path>
					</svg>
					换一换
				</button>
			</div>
		</div>

		<div id="zhihu-zaixian">
			<h2>在知乎创作</h2>
			<button class="lan">申请专栏</button>
		</div>
		<div class="end">
			<h4>© 2020 知乎 · 知乎专栏 · 圆桌·发现 · 移动应用 · 使用机构帐号登录 · 联系我们 · 来知乎工作</h4>
			<h4>
				京 ICP 证 110745 号 · 京 ICP 备 13052560 号 - 1 ·
				<img src="https://pic3.zhimg.com/80/v2-d0289dc0a46fc5b15b3363ffa78cf6c7.png" />
				京公网安备 11010802010035 号 · 出版物经营许可证
			</h4>
		</div>
	</div>
</template>

<script>
export default {
	name: 'columns',
	data() {
		return {
			columns: [],
			count: 8,
			currentPage: 2
		};
	},
	created() {
		this.axios({
			method: 'post',
			url: 'http://localhost:8080/api/columns/page',
			params: {
				count: this.count,
				currentPage: this.currentPage
			}
		}).then(res => {
			console.log(res.data.data);
			this.columns = res.data.data;
			console.log(this.columns.length);
		});
	},
	methods: {
		loadMore() {
			this.currentPage = this.currentPage + 1;
			this.axios({
				method: 'post',
				url: 'http://localhost:8080/api/columns/page',
				params: {
					count: this.count,
					currentPage: this.currentPage
				}
			}).then(res => {
				console.log(res.data.data);
				this.columns = res.data.data;
				console.log(this.columns.length);
			});
		}
	}
};
</script>

<style lang="scss" scoped>
.row {
	display: flex;
	flex-wrap: wrap;
}
.container {
	display: flex;
	background-color: rgb(251, 252, 252);
}
.con-left {
	width: 10%;
}
.con-right {
	width: 10%;
}
.container-top {
	background-image: url(../assets/image/topic.png);
	background-position: center;
	height: 470px;
	position: relative;
	text-align: center;
	z-index: 2;
}
.top-img {
	position: relative;
	top: 150px;
}
.container-top h3 {
	position: relative;
	top: 170px;
	font-weight: 300;
	letter-spacing: 5px;
}
.top-button {
	background-color: white;
	padding-top: 10px;
	padding-bottom: 10px;
	padding-left: 20px;
	padding-right: 20px;
	border: 1px solid black;
	border-radius: 5px;
	position: relative;
	top: 200px;
}
.con-home {
	width: 80%;
	text-align: center;
}
.con-home h5 {
	color: rgb(16, 156, 98);
	font-weight: 400;
}
.con-home h4 {
	margin-top: 20px;
	margin-bottom: 20px;
}
.column {
	width: 23%;
	background-color: white;
	margin: 10px;
	box-shadow: 1px 1px 5px #aaa;
	text-align: center;
	border-radius: 5px;
}
.column img {
	margin-top: 10px;
	margin-bottom: 10px;
	width: 80px;
	height: 80px;
	border-radius: 200px;
}
.column .title {
	text-overflow: -o-ellipsis-lastline;
	overflow: hidden;
	text-overflow: ellipsis;
	display: -webkit-box;
	-webkit-line-clamp: 1;
	-webkit-box-orient: vertical;
}
.column .description {
	color: darkgray;
	font-weight: 400;
	min-height: 40px;
	margin: 10px;
	text-overflow: -o-ellipsis-lastline;
	overflow: hidden;
	text-overflow: ellipsis;
	display: -webkit-box;
	-webkit-line-clamp: 2;
	-webkit-box-orient: vertical;
}
.column .follower {
	color: darkgray;
	font-weight: 400;
}
.column-button {
	margin: 20px;
	background-color: white;
	border: 1px solid rgb(17, 166, 104);
	border-radius: 5px;
	color: rgb(17, 166, 104);
	padding-top: 10px;
	padding-bottom: 10px;
	padding-left: 15px;
	padding-right: 15px;
}
.column-button:hover {
	background-color: rgb(241, 250, 246);
}
.change-button {
	border: 1px solid black;
	background-color: white;
	padding-top: 5px;
	padding-bottom: 5px;
	padding-left: 15px;
	padding-right: 15px;
	border-radius: 5px;
	margin: 20px;
}
.change-button:hover {
	background-color: rgb(244, 245, 247);
}
#zhihu-zaixian {
	width: 100%;
	height: 450px;
	background: white;
	background-image: linear-gradient(white 14px, transparent 0), linear-gradient(90deg, darkgray 1px, transparent 0);
	background-size: 10px 15px;
	text-align: center;
}
#zhihu-zaixian h2 {
	position: relative;
	top: 150px;
	font-weight: 200;
	letter-spacing: 10px;
	border-top: 1px solid rgb(151, 255, 216);
	border-bottom: 1px solid rgb(151, 255, 216);
	padding: 30px;
	margin-left: 420px;
	margin-right: 420px;
}
.lan {
	border: 1px solid black;
	border-radius: 5px;
	font-size: 20px;
	background-color: rgba(255, 255, 255, 0);
	padding-top: 5px;
	padding-bottom: 5px;
	padding-left: 20px;
	padding-right: 20px;
	position: relative;
	top: 200px;
}
.end {
	text-align: center;
	background-color: white;
	margin-bottom: 150px;
}
.end h4 {
	color: gray;
	font-weight: 400;
	line-height: 40px;
}
#div8 {
	width: 100%;
	height: 400px;
	background: white;
	background-image: linear-gradient(white 14px, transparent 0), linear-gradient(90deg, black 1px, transparent 0);
	background-size: 10px 15px, 15px 15px;
	position: absolute;
	z-index: 1;
	opacity: 0.1;
}
.zhuanlan-write-btn{
		width: 11%;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
	
	.zhuanlan-header {
		position: sticky;
		height: 50px;
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
		background-color: #FFFFFF;
		border-bottom: 1px solid #C4C4C4;
		display: block;
		display: flex;
		position:fixed;
	}
	
	.zhuanlan-header-content{
		width: 70%;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
	
	.write-psgs{
		border: 1px solid #0084FF;
		width: 95px;
		height: 30px;
		display: flex;
		justify-content: center;
		align-items: center;
		border-radius: 5px;
		color: #0084FF;
		font-size: 15px;
	}
	
	.write-psgs:hover{
		background-color: rgb(240,248,255);
		cursor: pointer;
	}
	.more{
		fill: #8590a6;
		margin-left: 15px;
		top: 50%;
	}
</style>
