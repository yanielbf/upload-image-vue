# Upload-image-vue

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

View example in codesanbox
https://codesandbox.io/s/epic-river-zp6et?file=/src/App.vue

```vue
<template>
  <div id="app">
    <upload-image-vue
      v-bind:loading="loading"
      v-bind:files="files"
      v-bind:callbackUpload="upload"
      v-bind:callbackDelete="remove"
    />
  </div>
</template>

<script>
import UploadImageVue from "upload-image-vue";
import "upload-image-vue/dist/lib/upload-image-vue.min.css";

export default {
  name: "App",
  data() {
    return {
      files: [],
      loading: false,
    };
  },
  methods: {
    upload: async function (data) {
      this.loading = true;
      setTimeout(() => {
        this.files = this.files.concat([
          { id: 1, url: "https://via.placeholder.com/150" },
          { id: 2, url: "https://via.placeholder.com/150" },
          { id: 3, url: "https://via.placeholder.com/150" },
        ]);
        this.loading = false;
      }, 3000);
    },
    remove: async function (id) {
      this.files = this.files.filter((item) => item.id != id);
    },
  },
  components: {
    UploadImageVue,
  },
};
</script>

<style>
</style>

```