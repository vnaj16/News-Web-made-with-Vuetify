<template>
  <v-app>
    <SideMenu v-bind:api-key="apiKey" v-bind:drawer="drawer"></SideMenu>
    <v-app-bar fixed app clipped-left color="primary" dark class="elevation-2">
      <v-app-bar-nav-icon @click="drawer=!drawer" class="white--text">
      </v-app-bar-nav-icon>
      <v-toolbar-title class="white--text">Catch Up</v-toolbar-title>
    </v-app-bar>

    <v-content>
      <v-container fluid>
        <MainContent v-bind:articles="articles"></MainContent>
      </v-container>
    </v-content>
    <v-footer class="secondary" app>
      <v-layout row wrap align-center>
        <v-flex xs12>
          <div class="white--text ml3">
            Made with <v-icon class="red--text">favorite</v-icon>
            by Web Applications Development Team
            using <a class="white--text" href="#">Vuetify</a>
          </div>
        </v-flex>
      </v-layout>
    </v-footer>
  </v-app>
</template>

<script>
import axios from 'axios'
import MainContent from "@/components/main-content";
import SideMenu from "@/components/side-menu";

export default {
  name: 'App',

  components: {
    SideMenu,
    MainContent
  },

  data () {
    return{
      drawer: false,
      apiKey: '45fd0472e76c49df846b905d002e8fdc',
      articles: [],
      errors: []
    }
  },
  created(){
    axios.get('https://newsapi.org/v2/top-headlines?sources=techcrunch&apiKey='+this.apiKey)
    .then(response =>{
      this.articles = response.data.articles;
      console.log('data: ');
      console.log(response.data.articles);
    })
    .catch( e=>{
      this.errors.push(e);
    })
  }

};
</script>
