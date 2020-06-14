<template>
  <div class="">
    <v-app-bar color="primary" dark app>
      <v-app-bar-nav-icon @click="drawer=!drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>Vuetify</v-toolbar-title>
    </v-app-bar>
  </div>
</template>

<script>
export default {
  name: 'AppHeader',
  data () {
    return {
      drawer: false
    }
  }
}
</script>
