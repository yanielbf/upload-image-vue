<template>
  <div id="app">
    <uploader-image 
      v-bind:loading="loading"
      v-bind:files="files"
      v-bind:callbackUpload="upload"
      v-bind:callbackDelete="remove"
    />
  </div>
</template>

<script>
import UploaderImage from './components/uploader'

export default {
  name: 'app',
  data(){
    return {
      files: [],
      loading: false,
    };
  },
  methods: {
    upload: async function(data){
      
      this.loading = true;
      setTimeout(() => {
        this.files = this.files.concat([
          {id: 1, url:"//s.fenicio.app/f2/tex/productos/1-sublimable_460x460_1537557205_cca.jpg"},
          {id: 2, url:"//s.fenicio.app/f2/tex/productos/1-sublimable_460x460_1537557205_cca.jpg"},
          {id: 3, url:"//s.fenicio.app/f2/tex/productos/1-sublimable_460x460_1537557205_cca.jpg"},
        ]);
        this.loading = false;
      }, 3000)   
    },
    remove: async function(id){
      this.files = this.files.filter(item => item.id != id);
    }
  },
  components: {
    UploaderImage
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
  margin-top: 60px;
  margin: 0 auto;
  width: 100%;
  padding-top: 30px;
}
</style>
