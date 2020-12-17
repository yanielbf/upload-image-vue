# Upload-image-vue

[![N|Otiumtek](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

### Getting Started

Upload-image-vue is a Vue component that allows you to upload images to a web server.

### Installation
Using npm:

```sh
$ npm install upload-image-vue --save
```
Using yarn:
```sh
$ yarn add upload-image-vue --save
```

### Usage example

```vue
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
import UploaderImage from 'upload-library'

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
          {id: 2, url:"//s.fenicio.app/f2/tex/productos/1-sublimable_460x460_1537557205_cca.jpg"}
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
  margin-top: 60px;
  margin: 0 auto;
  width: 100%;
  padding-top: 30px;
}
</style>
```