<template>
  <div>
    <v-app id="inspire">
          <v-navigation-drawer app v-model="navdrawer">
        <v-list-item class="ma-0 pa-0">
          <v-list-item-content class="ma-0 pa-0">
            <v-list-item-title class="title" >
              <v-img :aspect-ratio="16/9" src="https://i.imgur.com/BqEcjj4.png">
              <v-icon 
                x-large
                class= "pa-1"
                color="white "
                @click="navdrawer = !navdrawer"
              >mdi-chevron-left</v-icon>
              </v-img>
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
  
        <v-divider></v-divider>
  
        <v-list
          dense
          nav
        >
          <v-list-item
            v-for="item in drawerItems"
            :key="item.title"
            :to="item.to"
          >
            <v-list-item-icon>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-icon>
  
            <v-list-item-content>
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-divider></v-divider>
          <v-list-item
            v-for="item in drawerEtcItems"
            :key="item.title"
            :to="item.to"
          >
            <v-list-item-icon>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-icon>
  
            <v-list-item-content>
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-navigation-drawer>
      

      <v-speed-dial   
      top
      right
      absolute
      direction="left"
      transition='slide-x-reverse-transition'>
      <template v-slot:activator>
        <v-btn
          color="#97b300"
          dark
          fab
        >
          <v-icon >
            mdi-plus
          </v-icon>
        </v-btn>
      </template>

      <template v-if="!email"> 
              <v-btn
        to="/signin"
        fab
        dark
        small
        color="#97b300"
      >
        <v-icon>mdi-login</v-icon>
      </v-btn>
      </template>
      <template v-else>
      <v-btn

        @click="logout"
        fab
        dark
        small
        color="#97b300"
      >
        <v-icon>mdi-logout</v-icon>
      </v-btn>
      </template>

      <v-btn
        to="/my-diet"
        fab
        dark
        small
        color="#97b300"
      >
        <v-icon>mdi-calendar-month</v-icon>
      </v-btn>
      <v-btn
        to="/"
        fab
        dark
        small
        color="#97b300"
      >
        <v-icon>mdi-home</v-icon>
       </v-btn>
   



      </v-speed-dial>




      <div>
        <nuxt style="background-color: #f2f2f2;"/>
      </div>
      <div>
        <v-footer
          dark
          padless
        >
          <v-layout row wrap 
            class="mx-0">
            <v-flex xs12 class="text-center">
              <v-card
                color="#3d3d3d"
                flat
                >

                <v-card-text>
                  <v-btn
                    v-for="f_item in footerItems"
                    :key="f_item.icon"
                    :href="f_item.href"
                    class="mx-2 white--text"
                  >
                    <v-icon size="24px">{{ f_item.icon }}</v-icon>
                  </v-btn>
                </v-card-text>
                <v-card-text class="white--text pt-0">
                  <p>
                    <span>캡스톤 2조 </span>
                    
                  </p>
                  <p>
                    <span>소스코드는 </span>
                    <a href="https://github.com/peterhyun1234/My_nutrition_mate" style="text-decoration:none">
                      <strong>
                        <span style="color: #919191;">Github repository</span>
                      </strong>
                    </a>
                    <span>에 올려뒀고, 개발 관련 지식이나 도움이 필요하신 분들은 이메일로 연락주길 바랍니다 :D</span>
                  </p>
                </v-card-text>

                <v-divider></v-divider>

                
              </v-card>
            </v-flex>
          </v-layout>
        </v-footer>
        </div>
          <v-bottom-navigation
            background-color="#97b300"
            dark
            shift
            grow
            fixed
          >
     <v-btn to="/recomendation/weeks">
      <span>식단 추천</span>

      <v-icon>mdi-food-apple</v-icon>
     </v-btn>

     <v-btn to="/my-diet">
      <span>식단 기록</span>

      <v-icon>mdi-calendar-month</v-icon>
     </v-btn>

     <v-btn>
      <span>식단 관리사</span>

      <v-icon>mdi-wechat</v-icon>
     </v-btn>

     <v-btn to="/community">
      <span>커뮤니티</span>

      <v-icon>mdi-account-group</v-icon>
     </v-btn>

     <v-btn to="/recomendation/food">
      <span>동네 맛집</span>

      <v-icon>mdi-cart</v-icon>
     </v-btn>

   </v-bottom-navigation>
      
    </v-app>
  </div>
  
</template>

<script>
export default {
  components: {
  },
  data () {
    return {
      navdrawer: true,
      isUpdated: false,
      drawerItems: [
        { title: '내 식단 확인', icon: 'mdi-ticket-account', to: '/my-diet'},
        { title: '식단 추천', icon: 'mdi-food', to: '/recomendation/weeks'},
        { title: '메뉴 추천', icon: 'mdi-food-variant', to: '/recomendation/food'},
      ],
      drawerEtcItems: [
        { title: '커뮤니티', icon: 'mdi-sprout' , to: '/community'},
      ],
      footerItems: [
        { icon: 'mdi-github' , href: 'https://github.com/joon7324/DanChoo'},
      ],
      email: "",
    }
  },
  updated() {
    console.log("updated")
    const recievedID = localStorage.getItem("ID");
    const parsedID = JSON.parse(recievedID);
    this.email = parsedID
  },
  created(){
    //console.log("created")
    //console.log('created navdrawer: ' + this.navdrawer)
  },
  mounted()
  {
    //console.log("mounted")
  },
  destroyed(){
    console.log("destroyed")
  },
  methods: {
    // async signOut() {
    //   try {
    //     await this.$auth().signOut()
    //     this.$router.push('/')
    //   } catch (e) {
    //     console.error(e.message)
    //   }
    // },
    callUpdate(){
      //console.log("callUpdate")
      
      if(this.isUpdated == false){
        this.isUpdated = true;
      }
      else{
        this.isUpdated = false;
      }
    },
    logout(){
      localStorage.removeItem('ID');
      alert("로그아웃 완료!");
    }
  }
}
</script>

<style>
html {
  font-family: "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}
*, *:before, *:after {
  box-sizing: border-box;
  margin: 0;
}
.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;
}
.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}
.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}
.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}
</style>