<template>
  <v-navigation-drawer v-model="drawer" fixed app
  clipped class="drawer-style">
    <v-list dense class="pt-3 white--text">
      <v-list-item v-for="source in sources" :key="source.id"
                   @click="selectSource(source.id)">
      <v-list-item-action>
        <v-avatar size="32px">
          <v-img class="img-circle elevation-7 mv-1"
                 :src="getUrlToLogo(source)"
                 :alt="source.name"/>
        </v-avatar>
      </v-list-item-action>
        <v-list-item-content>
          <v-list-item-title>{{source.name}}</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </v-navigation-drawer>
</template>

<script>
import axios from 'axios'
export default {
 name: "side-menu",
  props:{
   apiKey: String,
    drawer: Boolean
  },
  data(){
    return{
      sources: [],
      errors: []
    }
  },
  created(){
   axios.get('https://newsapi.org/v2/sources?language=en&apiKey='
   +this.apiKey)
    .then(response=>{
      this.sources = response.data.sources;
      console.log('result: ');
      console.log(response.data.sources);
    })
    .catch(e=>{
      this.errors.push(e);
    })
  },
  methods:{
   selectSource(sourceId){
     this.$emit('select-source', sourceId);
   },
    getUrlToLogo(source){
     const HOSTNAME = new URL(source.url).hostname;
     return 'https://logo.clearbit.com/'+HOSTNAME;
    }
  }
}
</script>

<style scoped>

</style>