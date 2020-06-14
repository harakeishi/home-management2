<template>
  <div class="">
    <v-navigation-drawer app v-model="drawer" clipped>
      <v-container>
        <v-list-item>
          <v-list-item-content>
            <v-list-item-title class="title grey--text text--darken-2">
              MENU
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-divider></v-divider>
        <v-list dense nav>
          <v-list-item v-for="nav_list in nav_lists" :key="nav_list.name" @click="test(nav_list.path)">
            <v-list-item-icon>
              <v-icon>{{ nav_list.icon }}</v-icon>
            </v-list-item-icon>
            <v-list-item-title>{{ nav_list.name }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-container>
    </v-navigation-drawer>
    <v-app-bar color="primary" dark app clipped-left>
      <v-app-bar-nav-icon @click="drawer=!drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>ホームマネージメント</v-toolbar-title>
      <v-spacer></v-spacer>
      <span class="date">{{ time }}</span>
      <!--更新迄{{ Math.floor(reloadTime/60)}}分-->
    </v-app-bar>
    <v-content>
      <router-view />
    </v-content>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {
  },
  data () {
    return {
      drawer: true,
      nav_lists: [
        { name: '電気', icon: 'fas fa-lightbulb', path: '/' },
        { name: '天気', icon: 'fas fa-cloud-sun', path: '/weather' }
      ],
      time: new Date(),
      reloadTime: 3600
    }
  },
  omputed: {
    message: function () {
      return this.time.toLocaleString()
    }
  },
  methods: {
    test (link) {
      console.log(1)
      this.$router.push({ path: link })
    },
    refresh: function () {
      var crrentTime = new Date()
      var hour = crrentTime.getHours() // 時
      var min = crrentTime.getMinutes() // 分
      var sec = crrentTime.getSeconds() // 秒
      if (hour < 10) { hour = '0' + hour }
      if (min < 10) { min = '0' + min }
      if (sec < 10) { sec = '0' + sec }
      this.time = hour + ':' + min + ':' + sec
      const self = this
      setTimeout(() => { self.refresh() }, 1000)
    }
  },
  created: function () {
    this.refresh()
    setInterval(() => { this.reloadTime-- }, 1000)
  },
  watch: {
    reloadTime: function (v) {
      if (v <= 0) {
        document.location = '/'
      }
    }
  }
}
</script>
<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  position: fixed;
  margin-top: -10px;
}
#nav{
  background-color: rgb(3, 89, 217);
  font-size: 3vh;
  font-weight: bold;
  color: white;
}
.date{
  float: right;
  font-family: 'DS-DIGIT';
  font-weight: bold;
  font-size: 8vh;
  color: rgb(255, 174, 15);
  font-weight: bold;
}
</style>
