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

  .upload-container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
    grid-column-gap: 6px;
    grid-row-gap:6px;
    justify-items: center;
  }

  .upload-image-preview {
    box-shadow: 0 0 25px -3px rgb(34 34 34 / 45%);
    height: 100px;
    width: 150px;
    position: relative;
    margin: 10px;
  }

  .upload-image-preview .image-item{
    width: 100%;
    height: 100%;
  }

  .upload-image-preview .icon-close{
    width: 18px;
    height: 18px;
    position: absolute;
    right: -9px;
    top: -9px;
    cursor: pointer;
  }

  .upload-zone-click {
    border: 1px dashed #CCC;
    border-radius: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100px;
    width: 150px;
    margin: 10px;
    position: relative;
    transition: background-color 0.5s ease;
  }

  .upload-zone-click .add-icon{
    width: 1.6rem;
    height: 1.6rem;
  }

  .upload-zone-click input {
    width: 100%;
    height: 100%;
    opacity: 0;
    cursor: pointer;
    position: absolute;
  }

  .upload-zone-click:hover {
    background-color: #eee;
  }

</style>
