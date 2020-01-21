<!-- <template>
	<div class="index-container">
		<div class="header">
			<div class="nav">
				<div style="display: flex;align-items: center;width: 85%;">
					<router-link to="/recommend" class="zh-logo"><img src="../../../vue-router-zhihu/src/assets/知乎.png" height="30px"
						 width="80px" /></router-link>
					<div class="sub-nav">
						<router-link to="/recommend" class="sub-nav-content1">首页</router-link>
						<router-link to="/day_hot" class="sub-nav-content">发现</router-link>
						<router-link to="/movie" class="sub-nav-content">话题</router-link>
					</div>
					<div class="search">
						<input type="text" placeholder="离职小编称IT之家评测收钱" />
						<div style="display: flex;width: 20%;justify-content: center;align-items: center;">
							<img src="../../../vue-router-zhihu/src/assets/zh-search.png" width="25px" height="25px" />
						</div>
					</div>
					<div class="question" @click="question">提问</div>
				</div>
				<div class="my-nav">
					<img src="../assets/bell.png" height="25px" width="25px" />
					<img src="../assets/私信.png" height="25px" width="25px" />
					<img :src="userInfo.avatar" width="35px" style="border-radius: 5px;" />
				</div>
			</div>
		</div>
		<div class="index-content">
			<div class="left-content">
				<div class="header-left">
					<div style="box-sizing: border-box; display: flex;width:22%;height: 100%;justify-content:space-between;align-items: center; margin-left: 3%;">
						<div :class="[currentId==index+1?'pages-active':'pages']" v-for="(title,index) in titles" :key="index" @click="tabchange(title)">
							<router-link :to="title.path" class="sub-pages">{{title.name}}</router-link>
						</div>
					</div>
				</div>
				<div class="page-content">
					<router-view />
				</div>
			</div>
			<div class="right-content">
				<div class="sub1">
					<div class="tabs">
						<div class="tab-item" v-for="(tab,index) in tabs" :key="index">
							<img :src="tab.img" width="20px" height="20px" />
							<router-link :to="tab.path" class="tab-name">{{tab.name}}</router-link>
						</div>
					</div>
				</div>
				<div class="sub2">
					<div class="lists">
						<div class="list-item" v-for="(list,index) in lists" :key="index" @mouseenter="inhover(list)" @mouseleave="leave(list)">
							<img :src="list.img" width="25px" height="25px" />
							<router-link target="_blank" :to="list.path" class="list-name">{{list.name}}</router-link>
						</div>
					</div>
				</div>
				<div class="sub3">
					<div class="item">
						<div class="sub-item" v-for="(item,index) in items" :key="index">
							<img :src="item.img" width="20px" height="20px" />
							<router-link :to="item.path" class="item-name">{{item.name}}</router-link>
						</div>
					</div>
				</div>
				<div class="sub4">
					<div class="sub4-nav">
						<div class="nav-sub">刘看山&nbsp;·&nbsp;</div>
						<div class="nav-sub">知乎指南&nbsp;·&nbsp;</div>
						<div class="nav-sub">知乎协议&nbsp;·&nbsp;</div>
						<div class="nav-sub">知乎隐私保护指引</div>
					</div>
					<div class="sub4-nav">
						<div class="nav-sub">应用&nbsp;·&nbsp;</div>
						<div class="nav-sub">工作&nbsp;·&nbsp;</div>
						<div class="nav-sub">申请开通知乎机构号</div>
					</div>
					<div class="sub4-nav">
						<div class="nav-sub">侵权举报&nbsp;·&nbsp;</div>
						<div class="nav-sub">网上有害信息举报专区</div>
					</div>
					<div class="sub4-nav">
						<div style="font-size: 13px;color: #8A8A8A;">违法和不良信息举报：010-82716601</div>
					</div>
					<div class="sub4-nav">
						<div class="nav-sub">儿童色情信息举报专区</div>
					</div>
					<div class="sub4-nav">
						<div class="nav-sub">电信与服务业务经营许可证</div>
					</div>
					<div class="sub4-nav">
						<div class="nav-sub">网络文化经营许可证</div>
					</div>
					<div class="sub4-nav">
						<div class="nav-sub">联系我们&nbsp;</div>
						<div style="font-size: 13px;color: #8A8A8A;">© 2019 知乎</div>
					</div>
				</div>
			</div>
		</div>
		<div class="index-overlay" v-if="show">
			<div class="index-overlay-content">
				<div class="left-index-overlay-content">
					<div class="left-index-overlay-content-info">
						<div style="width: 100%;display: flex;">
							<img src="../assets/my_avatar.jpg" width="50px" height="50px" style="margin-right: 12px;border-radius: 4px;" />
							<textarea placeholder="写下你的问题,准确地描述问题更容易得到解答" class="index-textarea"></textarea>
						</div>
						<div style="display: flex;justify-content: space-between;align-items: center;">
							<div style="display: flex;align-items: center;color: #8A8A8A;font-size: 13px;">
								<input type="radio" style="margin-right: 8px;" />匿名提问
							</div>
							<div class="release-question">发布问题</div>
						</div>
					</div>
				</div>
				<img src="../assets/cancel.png" width="25px" height="25px" style="margin: 25px;" @click="closequestion" />
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		name: 'Index',
		data() {
			return {
				userInfo: '',
				show: false,
				currentId: 1,
				titles: [{
						id: 1,
						name: '推荐',
						path: '/recommend'
					},
					{
						id: 2,
						name: '关注',
						path: '/follow'
					},
					{
						id: 3,
						name: '热榜',
						path: '/hot'
					}
				],
				tabs: [{
						img: '../../static/img/answersheet.png',
						name: '写回答',
						path: '/write'
					},
					{
						img: "../../static/img/write.png",
						name: '写文章',
						path: '/write'
					},
					{
						img: '../../static/img/centermyidea.png',
						name: '写想法',
						path: '/write'
					}
				],
				lists: [{
						id: 1,
						img: '../../static/img/flash.png',
						name: 'Live',
						color: 'rgb(255,207,0)',
						path: '/live'
					},
					{
						id: 2,
						img: '../../static/img/book.png',
						name: '书店',
						color: 'rgb(67,212,128)',
						path: '/categories'
					},
					{
						id: 3,
						img: '../../static/img/turntable2.png',
						name: '圆桌',
						color: 'rgb(0,132,255)',
						path: '/round_table'
					},
					{
						id: 4,
						img: '../../static/img/pencil.png',
						name: '专栏',
						color: 'rgb(15,136,235)',
						path: '/zhuanlan'
					},
					{
						id: 5,
						img: '../../static/img/money.png',
						name: '付费咨询',
						color: 'rgb(84,120,240)',
						path: '/consult_answer'
					}
				],
				items: [{
						img: '../../static/img/star.png',
						name: '我的收藏',
						path: '/follow_collection'
					},
					{
						img: '../../static/img/md_icon_question.png',
						name: '我关注的问题',
						path: '/follow_question'
					},
					{
						img: '../../static/img/invite.png',
						name: '我的邀请',
						path: '/recommend_for_you'
					},
					{
						img: '../../static/img/accountBalanceWallet.png',
						name: '我的余额',
						path: '/balance'
					},
					{
						img: '../../static/img/message.png',
						name: '站务中心',
						path: '/inform'
					},
					{
						img: '../../static/img/copyright.png',
						name: '版权服务中心',
						path: '/warrant'
					}
				]
			};
		},
		created() {
			this.userInfo = JSON.parse(window.localStorage.getItem("userinfo"));
		},
		methods: {
			tabchange(e) {
				var index = e.id;
				this.currentId = index;
			},
			inhover(list) {
				var index = list.id - 1;
				var x = document.querySelectorAll(".list-name");
				x[index].style.color = this.lists[index].color;
			},
			leave(list) {
				var index = list.id - 1;
				var x = document.querySelectorAll(".list-name");
				x[index].style.color = "#8A8A8A";
			},
			question(e) {
				this.show = true;
				document.querySelector(".index-container").style.height = "720px";
				document.querySelector(".index-container").style.overflowY = "hidden";
			},
			closequestion(e) {
				this.show = false;
				document.querySelector(".index-container").style.height = "100%";
				document.querySelector(".index-container").style.overflowY = "visible";
			}
		}
	};
</script>

<style>
	.header {
		position: fixed;
		top: 0;
		width: 100%;
		display: flex;
		align-items: center;
		height: 50px;
		background-color: #FFFFFF;
	}

	.index-content {
		width: 70%;
		min-height: 650px;
		display: flex;
		margin: 0 auto 0 auto;
		padding-top: 60px;
	}

	.nav {
		width: 70%;
		margin: 0 auto;
		display: flex;
		align-items: center;
		justify-content: space-between;
		height: 100%;
	}

	.sub-nav {
		width: 18%;
		height: 100%;
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-left: 35px;
		margin-right: 35px;
	}

	.sub-nav-content {
		text-decoration: none;
		color: #808080;
	}

	.sub-nav-content1 {
		text-decoration: none;
		color: #000000;
	}

	.sub-nav-content:hover {
		cursor: pointer;
		color: rgb(84, 120, 240);
	}

	.search {
		border-radius: 2px;
		width: 30%;
		display: flex;
		align-items: center;
		background-color: #E5E5E5;
		height: 40px;
	}

	.search input {
		width: 80%;
		height: 1.875rem;
		border: none;
		background-color: #E5E5E5;
		padding-left: 15px;
		font-size: 16px;
		outline: none;
	}

	.question {
		width: 55px;
		height: 40px;
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: rgb(0, 132, 255);
		color: #FFFFFF;
		border-radius: 5px;
		margin-left: 15px;
	}

	.question:hover {
		background-color: rgb(0, 119, 230);
		cursor: pointer;
	}

	.my-nav {
		height: 100%;
		width: 15%;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.my-nav img:hover {
		cursor: pointer;
	}

	.left-content {
		width: 70%;
		border-radius: 5px;
		background-color: #FFFFFF;
		display: flex;
		flex-direction: column;
		margin-right: 1%;
	}

	.right-content {
		width: 29%;
		border-radius: 5px;
		display: flex;
		flex-direction: column;
	}

	.sub1 {
		width: 100%;
		border-radius: 5px;
		background-color: #FFFFFF;
		margin-bottom: 3%;
	}

	.sub2 {
		border-radius: 5px;
		background-color: #FFFFFF;
		width: 100%;
		margin-bottom: 3%;
	}

	.sub3 {
		border-radius: 5px;
		background-color: #FFFFFF;
		width: 100%;
		margin-bottom: 3%;
		overflow: hidden;
		padding-top: 5px;
		padding-bottom: 5px;
	}

	.sub4 {
		width: 100%;
		display: flex;
		flex-direction: column;
	}

	.sub4-nav {
		display: flex;
		margin-bottom: 5px;
	}

	.nav-sub {
		font-size: 13px;
		color: #8A8A8A;
	}

	.nav-sub:hover {
		color: rgb(23, 81, 153);
		cursor: pointer;
	}

	.header-left {
		display: flex;
		width: 100%;
		height: 40px;
		align-items: center;
		border-bottom: 1px solid #E5E5E5;
	}

	.sub-pages:hover {
		cursor: pointer;
	}

	.sub-pages {
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		text-decoration: none;
		color: #000000;
		box-sizing: border-box;
	}

	.pages {
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		box-sizing: border-box;
	}

	.pages-active {
		height: 100%;
		box-sizing: border-box;
		display: flex;
		justify-content: center;
		align-items: center;
		font-weight: 800;
		text-decoration: none;
		color: #000000;
		border-bottom: 0.1875rem solid rgb(0, 132, 255);
	}

	.tabs {
		margin: 20px 0;
		display: flex;
		width: 100%;
		justify-content: space-between;
	}

	.tab-item {
		flex: 0 0 33.33%;
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	.tab-name {
		margin-top: 8px;
		text-decoration: none;
		color: #000000;
	}

	.lists {
		margin: 35px 0px 20px 0px;
		display: flex;
		width: 100%;
		justify-content: space-between;
		flex-wrap: wrap;
	}

	.list-item {
		flex: 0 0 33.33%;
		display: flex;
		flex-direction: column;
		align-items: center;
		margin-bottom: 15px;
	}

	.list-item:hover {
		cursor: pointer;
	}

	.list-item:last-child {
		margin-right: 33.33%;
	}

	.list-name {
		text-decoration: none;
		font-size: 15px;
		color: #8A8A8A;
		margin-top: 8px;
	}

	.item {
		display: flex;
		flex-direction: column;
		width: 100%;
		overflow: hidden;
	}

	.sub-item {
		width: 100%;
		height: 45px;
		padding-left: 20px;
		display: flex;
		align-items: center;
	}

	.sub-item:hover {
		cursor: pointer;
		background-color: rgb(246, 246, 246);
	}

	.item-name {
		font-size: 15px;
		color: #8A8A8A;
		margin-left: 10px;
		text-decoration: none;
	}

	.index-overlay {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(0, 0, 0, 0.4);
		display: flex;
		justify-content: center;
		z-index: 999;
	}

	.index-overlay-content {
		margin-top: 17%;
		width: 37%;
		display: flex;
	}

	.left-index-overlay-content {
		width: 88%;
		background-color: #FFFFFF;
		display: flex;
		flex-direction: column;
		border-radius: 2px;
		height: 270px;
		align-items: center;
		justify-content: center;
	}

	.left-index-overlay-content-info {
		width: 90%;
		height: 76%;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}

	.index-textarea {
		width: 81%;
		height: 150px;
		font-weight: 800;
		font-size: 17px;
		border: none;
		outline: none;
	}

	.release-question {
		width: 85px;
		height: 30px;
		display: flex;
		justify-content: center;
		align-items: center;
		color: #FFFFFF;
		border-radius: 4px;
		background-color: rgb(128, 194, 255);
	}
</style>
 -->