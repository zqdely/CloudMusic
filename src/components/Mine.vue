<template>
  <div class="mine">
      <div class="backs" @click="back"> 
        <img src="../../static/img/back.png" alt="">
      </div>
      <div class="out" @click="out">退出</div>
      <div class="mine-title" :style="titleStyle">
        <div class="mine-wrap">
          <div class="mine-img">
            <img :src="userData.profile.avatarUrl" alt="">
            <p class="mine-name" v-text="userData.profile.nickname"></p>
            <p class="mine-info">userId <span v-text="userData.profile.userId"></span></p>
            <p class="mine-info">createTime <span v-text="userData.account.createTime"></span></p>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
import { mapMutations, mapGetters } from 'vuex'
export default {
  data(){
    return{
      url:'',
      titleStyle:{
        backgroundImage: '',
        backgroundRepeat: "no-repeat",
        backgroundSize: "100% 5rem",
      }
    }
  },
  computed: {
    ...mapGetters([
      'userData'
    ]),
  },
  mounted(){
    if(!this.userData.first){
      this.titleStyle.backgroundImage='url('+this.userData.profile.backgroundUrl+')'
    }else{
      this.$router.replace('/login')
    }
  },
  methods:{
    back(){
      history.go(-1)
    },
    out(){
      window.sessionStorage.removeItem("userData");
      this.$store.commit('setUserData',{userData:{
        profile:{
          avatarUrl:'../../static/img/user.png',
          nickname:'',
          
        },
        account:{
          createTime:'',
        },
        first:true
      }});
      this.$store.commit('setReload',true);
      this.$router.replace('/')
    }
  }

    
}
</script>

<style>
.out{
  height: 1rem;
  line-height: 1rem;
  position: absolute;
  right: 0.5rem;
  color: #333;
  font-family: 'microsoft yahei'
}
.mine-title{
  width: 100%;
  height: 5rem;

}
.mine-wrap{
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,.2);
  display: flex;
  justify-content: center;
  align-items: center;
}
.mine-img{
  width: 100%;
  height: 100%;
  text-align: center;
  overflow: hidden;
}
.mine-img img{
  display: inline-block;
  width: 1.5rem;
  height: 1.5rem;
  border-radius: 0.75rem;
  margin: 1rem 0 0 0;
}
.mine-name{
  color: #fff;
  text-align: center;
  font-size: 16px;
}
.mine-info{
  width: 7.5rem;
  margin: 0.2rem;
  color: #fff;
}
</style>
