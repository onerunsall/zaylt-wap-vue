<template>
	<div class="user">
		<div class="user_top" :style="{'padding-top':$store.state.paddingTop}">
			<div class="user_set" v-show='false'>
				<img src="../../../assets/image/set up@2x.png" alt="" />
			</div>
			<div class="user_message">
				<div class="top_left">
					<img :src="coverImg? coverImg: require('../../../assets/image/logo@2x.png')" alt="">
					<!-- <span>已认证</span> -->
				</div>
				<div class="top_center">
					<h3>{{this.$store.state.operating.login? this.$store.state.operating.login.name:''}}</h3>
					<p>账号：{{this.$store.state.operating.login? this.$store.state.operating.login.phone:''}}</p>
				</div>
				<!-- <div class="top_right" @click="showImgFn">
					<span>营业执照</span>
					<img src="../../../assets/image/Chevron Copy 2@2x.png" alt="">
				</div> -->
			</div>
		</div>
		<!-- <van-image-preview v-model="show" :images="images" @change="onChange" > -->
		  <!-- <template v-slot:index>第{{ index }}页</template> -->
		</van-image-preview>
		<div class="user_center"  :style="{'padding-top': (parseInt($store.state.paddingTop.replace('px',''))+140)+'px'}">
			<ul>
				<li @click="exitFn">
					<span>退出登录</span>
					<img src="../../../assets/image/Chevron Copy 2@2x.png" alt="">
				</li>

			</ul>
		</div>
		<span>版本：{{this.$version.split('-')[0]}}</span>
    <!-- <div style="height: .55rem;"></div> -->
	</div>
</template>

<script>
import axios from 'axios'
import {mapActions,mapGetters} from 'vuex'
import qs from 'qs';
export default {
	name: 'user',
	data () {
		return {
			coverImg: '',
			show: false,
			index: 0,
			images: []
		}
  },
	computed:{
		// ...mapGetters(['account'])
		account: {
		    get: function() {
				// 
		        return this.$store.state.account
		    },
		    set: function (newValue) {
				this.$store.state.account = newValue;
		    },
		},
	},
	components:{
	},
	created(){
	},
 	mounted() {
		// if(window.plus){
		// 	//plus.navigator.setStatusBarBackground("#ffffff");
		// 	plus.navigator.setStatusBarStyle("dark")
		// }
		// if(this.$store.state.operating.login){
		// 	this.coverImg = this.$store.state.operating.login.cover
		// 	// this.images.push(this.$store.state.operating.login.hospital.license)
		// }
		// // 
		// this.initData();
	},
	activated(){
		if(this.query != JSON.stringify(this.$route.query)){
			this.initData();
			this.query = JSON.stringify(this.$route.query);
			if(window.plus){
				//plus.navigator.setStatusBarBackground("#ffffff");
				plus.navigator.setStatusBarStyle("dark")
			}
			if(this.$store.state.operating.login){
				this.coverImg = this.$store.state.operating.login.cover
				// this.images.push(this.$store.state.operating.login.hospital.license)
			}
		}
 	},
	methods: {
		initData(){
			let thisVue = this
			// if(this.$route.meta.auth && !this.$store.state.operating.login)
			// this.$toast({message:'请登录',onClose:function(){
			// 	thisVue.$router.replace({ path : '/operating/operatingLogin',query:{time:1}});
			// }})
		},
		onChange(index) {
		    this.index = index;
		},
		// showImgFn(){
		// 	this.show = true;
			
		// },
		//退出方法
		exitFn(){
			let thisVue=this
			this.$axios.post('/manager/logout').then(function(){
				localStorage.removeItem('entrance')
				// localStorage.clear()
				thisVue.$toast("操作成功")
				setTimeout(()=>{
					// thisVue.$router.push({path:"/operating/operatingLogin",query:{}})
					location.href=location.pathname
				},1500)
			})
			// if(window.plus){
			// 	plus.webview.currentWebview().clear()
			// 	//plus.webview.currentWebview().loadURL(aa)
			// }
			// location.href=location.pathname
			
		},
		noLinkFn(){
			this.$toast.setDefaultOptions({ duration: 1000 });
			this.$toast('升级中');
		}
	},
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.user{
	width: 100%;
	background-color: #F5F5F5;
}
.user_top{
	width: 100%;
	height: 1.3rem;
	background-color: #FFFFFF;
	/* margin-top: .36rem; */
	position: fixed;
	top:0;
	z-index: 999;
}
.user_set{
	top: .18rem;
	right: .16rem;
	position: absolute;
}
.user_set img{
	width: .21rem;
	height: .2rem;
}
.user_message{
	/* height: .8rem; */
	/* margin: auto 0rem; */
	/* padding: .23rem .18rem .15rem .28rem;; */
}

.top_left{
	width: 24%;
	float:left;
	height: .8rem;
	margin:.23rem .29rem .15rem .28rem;
}
.top_left img{
	width: .75rem;
	height: .75rem;
	position: relative;
	border-radius: 50%;
}
.top_left span{
	position: absolute;
	left: .61rem;
	/* top: .79rem; */
	bottom:.3rem;
	font-size: .03rem;
	color: #FFFFFF;
	background:url('../../../assets/image/Gradualchange@2x.png');
	background-size:100% 100%;
	padding: .02rem .1rem;
}
.top_center{
	position: relative;
	width: 33%;
	float: left;
	height: .49rem;
	margin: .37rem .16rem .28rem 0rem;
}
.top_center h3{
	height: .29rem;
	line-height: .29rem;
	font-size: .16rem;
	font-weight: bolder;
	font-weight: bolder;
	display: -webkit-box;
	overflow: hidden;
	text-overflow: ellipsis;
	word-wrap: break-word;
	-webkit-line-clamp: 1;
	-webkit-box-orient: vertical;
}
.top_center p{
	color: #666666;
	font-size: .13rem;
}
.top_right{
	width: 19%;
	float:left;
	margin: .53rem .14rem .44rem 0rem;
	color: #999999;
	position: relative;
}
.top_right img{

	width: .08rem;
	height: .13rem;
  position: absolute;
  height: .13rem;
  bottom: 0rem;
  top: 0rem;
  margin: auto 0rem;
}
.top_right span{
  margin-right: .1rem;
}
.user_center{
	width: 100%;
	position: fixed;
	height: calc(100% - 1.9rem);
	padding-top: 1.6rem;
}
.user_center ul{
	height: 100%;
	width: 100%;
	background-color: #FFFFFF;
	font-size: .14rem;
}

.user_center ul li{
	height: .52rem;
	line-height: .52rem;
	padding: 0rem .18rem;
	position: relative;
	border-bottom: 1px solid #EEEEEE;
}
.user_center ul a:last-child{
	margin-bottom: .5rem;
}
.user_center ul li img{
	position: absolute;
	height: .13rem;
	width: .08rem;
	right: .18rem;
	top: .19rem;
}
.user>span{
	width: 50%;
	text-align: center;
	color: #cfd2d3;
	position: absolute;
	bottom: .8rem;
	left: 0rem;
	right: 0rem;
	margin: 0rem auto;
}
</style>
