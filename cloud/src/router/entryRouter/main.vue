<template>
    <div class="container">
       <div class="top">
            <header-top></header-top>
            <!-- <login></login> -->
       </div>
       <div class="banner">
           <!-- 歌单推荐 -->
           <div class="swiperBox">
               <h1></h1>
                <el-carousel indicator-position="none" arrow='hover' :interval='4000'>
                    <el-carousel-item>
                        <div class="songsList_day" >
                            <ul>
                                <li v-for="list in dayList_1"  :id='list.id'>
                                     <router-link :to="{ name: 'musiclist', params: { listId: list.id }}" :listId='list.id'>
                                        <span>
                                            <img :src="list.picUrl" alt="">
                                            <i></i>
                                            <em></em>
                                        </span>
                                    <h2>{{ list.name }}</h2>
                                    <p>播放量 : {{ list.playCount }}</p>
                                     </router-link>
                                    
                                </li>
                            </ul>
                        </div>  
                    </el-carousel-item>
                    <el-carousel-item>
                        <div class="songsList_day">
                            <ul>
                                <li v-for="list in dayList_2"  :id='list.id'>
                                    <router-link :to="{ name: 'musiclist', params: { listId: list.id }}" :listId='list.id'>
                                   <span>
                                       <img :src="list.picUrl" alt="">
                                        <i></i>
                                        <em></em>
                                    </span>
                                    <h2>{{ list.name }}</h2>
                                    <p>播放量 : {{ list.playCount }}</p>
                                    </router-link>
                                </li>
                            </ul>
                        </div>  
                    </el-carousel-item>
                    <el-carousel-item>
                        <div class="songsList_day">
                            <ul>
                                <li  v-for="list in dayList_3" :id="list.id">
                                    <router-link :to="{ name: 'musiclist', params: { listId: list.id }}" :listId='list.id'>
                                   <span>
                                       <img :src="list.picUrl" alt="">
                                        <i></i>
                                        <em></em>
                                    </span>
                                    <h2>{{ list.name }}</h2>
                                    <p>播放量 : {{ list.playCount }}</p>
                                    </router-link>
                                </li>
                            </ul>
                        </div>  
                    </el-carousel-item>
                </el-carousel>
           </div>
       </div>
       <!-- //新歌推荐 -->
           <div class="swiperNewsongs">
               <div class="swiperBox">
                    <el-tabs type="card">
                        <el-tab-pane :label='index' v-for="index in ['内地','港台','欧美','其他']" :key='index'>
                            <ul>
                                <li v-for="songs in new_songs"  :id="songs.id" @click='$store.dispatch("getMusic", songs.id)'>
                                    <div class="songImg">
                                        <img :src="songs.song.album.picUrl" alt="">
                                        <span></span>
                                    </div>
                                    <div class="songInfo">
                                        <h1>{{songs.name}}</h1>
                                        <p>{{songs.song.album.artists[0].name}}</p>
                                    </div>
                                    <i></i>
                                </li>
                            </ul>
                        </el-tab-pane>
                    </el-tabs>
               </div>
           </div> 
           
           <!-- 排行榜 -->
           <div class="ranking">
                <h1></h1>
               <div class="rankingList">
                  <!-- 新歌排行榜 -->
                   <div class="rank_newSong">
                      <div class="rank_detail">
                         
                      </div>
                       <ul>
                           <h2>
                               <span>新歌</span>
                           </h2>
                            <div class="listIcon" @click='playAll(rank_newSong)'>
                                <em class="icon_line"></em>
                                <em class="icon_video"></em>
                            </div>
                            <div class="songsList">
                                <li v-for='(song,index) in rank_newSong'  :id="song.id">
                                    <h3>
                                        <i v-text='index+1'></i>
                                        <span v-text="song.name"></span>
                                    </h3>
                                    <p>
                                        <small v-for='(singer,index) in song.ar' v-text='song.ar.length>1&&index != song.ar.length-1?singer.name+"/":singer.name' >
                                        </small>
                                    </p>
                                </li>
                            </div>
                            
                        </ul>
                   </div>
                    <!-- 热门歌曲 -->
                   <div class="rank_hotSong">
                      <div class="rank_detail">
                          
                      </div>
                       <ul>
                           <h2>
                               <span>热歌</span>
                           </h2>
                            <div class="listIcon" @click='playAll(rank_hotSong)'>
                                <em class="icon_line"></em>
                                <em class="icon_video"></em>
                            </div>
                            <div class="songsList">
                                <li v-for='(song,index) in rank_hotSong'  :id="song.id" >
                                    <h3>
                                        <i v-text='index+1+"."'></i>
                                        <span v-text="song.name"></span>
                                    </h3>
                                    <p>
                                        <small v-for='(singer,index) in song.ar' v-text='song.ar.length>1&&index != song.ar.length-1?singer.name+"/":singer.name' >
                                        </small>
                                    </p>
                                </li>
                            </div>
                        </ul>                      
                   </div>
                   <div class="rank_UsaSong">
                      <div class="rank_detail">
                          
                      </div>
                       <ul>
                           <h2>
                               <span>英国UK榜</span>
                           </h2>
                            <div class="listIcon"  @click='playAll(rank_UsaSong)'>
                                <em class="icon_line"></em>
                                <em class="icon_video"></em>
                            </div>
                            <div class="songsList">
                                <li v-for='(song,index) in rank_UsaSong' :id="song.id">
                                    <h3>
                                        <i v-text='index+1+"."'></i>
                                        <span v-text="song.name"></span>
                                    </h3>
                                    <p>
                                        <small v-for='(singer,index) in song.ar' v-text='song.ar.length>1&&index != song.ar.length-1?singer.name+"/":singer.name' >
                                        </small>
                                    </p>
                                </li>
                            </div>
                        </ul>                       
                   </div>
                   <div class="rank_KoreaSong">
                      <div class="rank_detail">
                         
                      </div>
                       <ul>
                           <h2>
                               <span>韩国</span>
                           </h2>
                            <div class="listIcon" @click='playAll(rank_Korea)'>
                                <em class="icon_line"></em>
                                <em class="icon_video"></em>
                            </div>
                            <div class="songsList">
                                <li v-for='(song,index) in rank_Korea'  :id="song.id">
                                    <h3>
                                        <i v-text='index+1+"."'></i>
                                        <span v-text="song.name"></span>
                                    </h3>
                                    <p>
                                        <small v-for='(singer,index) in song.ar' v-text='song.ar.length>1&&index != song.ar.length-1?singer.name+"/":singer.name' >
                                        </small>
                                    </p>
                                </li>
                            </div>
                        </ul>                       
                   </div>
                   <div class="rank_itunes">
                      <div class="rank_detail">
                                    
                      </div>
                        <ul>
                           <h2>
                               <span>iTunes</span>
                           </h2>
                            <div class="listIcon" @click='playAll(rank_iTunes)'>
                                <em class="icon_line"></em>
                                <em class="icon_video"></em>
                            </div>
                            <div class="songsList">
                                <li v-for='(song,index) in rank_iTunes'  :id="song.id">
                                    <h3>
                                        <i v-text='index+1+"."'></i>
                                        <span v-text="song.name"></span>
                                    </h3>
                                    <p>
                                        <small v-for='(singer,index) in song.ar' v-text='song.ar.length>1&&index != song.ar.length-1?singer.name+"/":singer.name' >
                                        </small>
                                    </p>
                                </li>
                            </div>
                        </ul>                       
                   </div>
               </div>
           </div>
    </div>
  
</template>
<script>
import headerTop from "../../components/headerTop";

import store from "../../store/store";
import { mapMutations } from "vuex";
import { mapActions } from "vuex";
export default {
  data() {
    return {
      dayList_1: [], //sweper1
      dayList_2: [], //swiper2
      dayList_3: [], //swiper3
      new_songs: [], //新歌推荐
      rank_newSong: [], //新歌排行榜
      rank_hotSong: [], //热歌排行榜
      rank_UsaSong: [], //UK排行榜
      rank_Korea: [], //韩国排行榜
      rank_iTunes: [] //Itunes榜单
    };
  },
  components: {
    headerTop,
  },
  methods: {
    ...mapActions([
      "getUserwatch",
      "getMusic",
      ]),
    getDayList() {
      //每次推荐歌单
      this.$http.get(BASE + "/personalized").then(data => {
        let result = data.data.result;
        this.dayList_1 = result.slice(0, 5);
        this.dayList_2 = result.slice(5, 10);
        this.dayList_3 = result.slice(10, 15);
      });
      //新歌推荐
      this.$http.get(BASE + "/personalized/newsong").then(data => {
        this.new_songs = data.data.result.slice(0, 9);
      });
      this.$http
        .get(BASE + "/top/list?idx=0")
        .then(({ data: { code, playlist } }) => {
          if (code == 200) {
            this.rank_newSong = playlist.tracks.slice(0, 10);
          }
        });
      this.$http
        .get(BASE + "/top/list?idx=1")
        .then(({ data: { code, playlist } }) => {
          if (code == 200) {
            this.rank_hotSong = playlist.tracks.slice(0, 10);
          }
        });
      this.$http
        .get(BASE + "/top/list?idx=5")
        .then(({ data: { code, playlist } }) => {
          if (code == 200) {
            this.rank_UsaSong = playlist.tracks.slice(0, 10);
          }
        });
      this.$http
        .get(BASE + "/top/list?idx=11")
        .then(({ data: { code, playlist } }) => {
          if (code == 200) {
            this.rank_Korea = playlist.tracks.slice(0, 10);
          }
        });
      this.$http
        .get(BASE + "/top/list?idx=8")
        .then(({ data: { code, playlist } }) => {
          if (code == 200) {
            this.rank_iTunes = playlist.tracks.slice(0, 10);
          }
        });
    },
    playAll: function(songsArr){  //播放全部
      let that = this;
      that.$store.state.list_id = [];
      songsArr.map((val,index) => {
       that.$store.state.list_id.push(val.id);
    })
     that.$store.state.CURPLAYLIST = songsArr;
     that.$store.dispatch("getMusic", that.$store.state.list_id[0])
    },
  },
  mounted() {
    this.getDayList();
  }
};
</script>



<style lang='less' scoped>
@import url("../../assets/less/main.less");
</style>
<style lang='less'>
.el-carousel__arrow {
  width: 50px;
  height: 100px;
  border-radius: 5px;
}
.el-carousel__arrow--right {
  right: 0;
  & i:after,
  & i:before {
    content: "";
  }
  i {
    background: url("../../assets/images/arrow-left.png") no-repeat;
    width: 32px;
    height: 32px;
  }
}
.el-carousel__arrow--left {
  left: 0;
  & i:after,
  & i:before {
    content: "";
  }
  i {
    background: url("../../assets/images/arrow-right.png") no-repeat;
    width: 32px;
    height: 32px;
  }
}
.el-tabs--card > .el-tabs__header .el-tabs__nav {
  border: none;
  float: none;
  text-align: center;
  .el-tabs__item {
    border: none;
    font-size: 15px;
  }
  .el-tabs__item.is-active,
  .el-tabs__item:hover {
    color: #31c27c;
  }
}
.el-tabs--card > .el-tabs__header {
  border: none;
}
</style>