<template>
    <div id="detailContrainer" class="slide-enter-active">
        <Header title="影片详情">
            <i class="iconfont  icon-right" @touchstart="handleToBack"></i>
        </Header>
        <div id="content" class="contentDetail">
            <div class="detail_list">
                <div class="detail_list_bg"></div>
                <div class="detail_list_filter"></div>
                <div class="detail_list_content">
                    <div class="detail_list_img">
                        <img :src="detailMovie.img | setWH('148.208')" alt="">
                    </div>
                    <div class="detail_list_info">
                        <h2>{{ detailMovie.nm }}</h2>
                        <p>{{ detailMovie.enm }}</p>
                        <p>{{ detailMovie.sc }}</p>
                        <p>{{ detailMovie.cat }}</p>
                        <p>{{ detailMovie.src }} / {{ detailMovie.dur }}</p>
                        <p>{{ detailMovie.pubDesc }}</p>
                    </div>
                </div>
            </div>
            <div class="detail_intro">
                <p>待完善</p>
            </div>
        </div>
    </div>
</template>

<script>
import Header from '@/components/Header'

export default {
    name: 'detail',
    data(){
        return{
            detailMovie:{}
        }
    },
    components:{
        Header
    },
    props:['movieId'],
    methods:{
        handleToBack(){
            this.$router.back();
        }
    },
    mounted(){
        this.axios.get('/api/detailMovie?movieId='+this.movieId).then((res)=>{
            var msg = res.data.msg;
            if(msg === 'ok'){
                this.detailMovie = res.data.data.detailMovie;
            }
        })
    }
}
</script>

<style scoped>
#detailContrainer{position: absolute;left: 0;top: 0;z-index: 999;width: 100%;min-height: 100%;background: white;}
.slide-enter-active{animation: .5s slideMove;}
@keyframes slideMove {
    0%{transform: translateX(100%);}
    100%{transform: translateX(0)}
}
#content.contentDetail{display:block;margin-bottom:0}
#content .detail_list{height:200px;width:100%;position:relative;overflow:hidden}
.detail_list .detail_list_bg{width:100%;height:100%;background:0 40%;filter:blur(20px);background-size:cover;position:absolute;left:0;top:0}
.detail_list .detail_list_filter{width:100%;height:100%;background-color:#40454d;opacity:.55;position:absolute;left:0;top:0;z-index:1}
.detail_list .detail_list_content{display:flex;width:100%;height:100%;position:absolute;left:0;top:0;z-index:2}
.detail_list .detail_list_img{width:108px;height:150px;border:1px solid #f0f2f3;margin:20px}
.detail_list .detail_list_img img{width:100%;height:100%}
.detail_list .detail_list_info{margin-top:20px}
.detail_list .detail_list_info h2{font-size:20px;color:#fff;font-weight:400;line-height:40px}
.detail_list .detail_list_info p{color:#fff;line-height:20px;font-size:14px;color:#ccc}

#content .detail_intro{padding: 10px;text-align: center;}
</style>
