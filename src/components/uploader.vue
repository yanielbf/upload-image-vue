<template>
  <div class="upload-container">
    <div v-for="file in files" :key="file.id" class="upload-image-preview">
      <img v-on:click="() => handleRemoveFileUploaded(file.id)" class="icon-close" src="../assets/icon-close@3x.png" />
      <img class="image-item" :src="file.url" />
    </div>
    <div class="upload-zone-click">
      <input v-if="!loading" type="file" id="files" ref="files" multiple v-on:change="handleFilesToUpload()" accept="image/x-png,image/gif,image/jpeg" />
      <img v-if="!loading" class="add-icon" src="../assets/group-19@3x.png" />
      <img v-if="loading" class="add-icon" src="https://covid19healthcheck.powerappsportals.com/spinner.gif" />
    </div>
  </div>
</template>

<script>

export default {
  props: {
    loading:{
      default: false
    },
    files:{
      default: [],  
    },
    callbackUpload: {
        default: () => null,
    },
    callbackDelete: {
        default: () => null,
    },
  },
  data () {
    return {
      filesToUpload: [],
    }
  },
  methods: {
    handleFilesToUpload: async function() {
      let uploadedFiles = this.$refs.files.files;
      for( var i = 0; i < uploadedFiles.length; i++ ){
        this.filesToUpload.push( uploadedFiles[i] );
      }
      let formData = new FormData();
      for( var i = 0; i < this.filesToUpload.length; i++ ){
        let file = this.filesToUpload[i];
        formData.append('files[' + i + ']', file);
      }
      if(this.callbackUpload){
        this.callbackUpload(formData);
      }
    },
    handleRemoveFileUploaded: async function(id) {
      if(this.callbackDelete){
        this.callbackDelete(id);
      }
    }
  }
}
</script>

<style scoped>

</style>
