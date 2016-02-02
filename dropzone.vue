<style scoped>
.dropzone{
  position: relative;
  margin: 16px;
}
.dropzone > .filezone{
  width: 100%;
  height: 100%;
  opacity: 0;
}
.dropzone > .zone{
  display: flex;
  align-items: center;
  justify-content: center;
  pointer-events: none;
  overflow: auto;
}
</style>

<template>
  <div class="dropzone" :style="{'height': height }">
    <input type="file" name="files" class="filezone full-width" title="Dropzone" multiple @change="getFiles">
    <div class="zone stretch">
      <span class="message" v-show="!files.length">{{ message }}</span>
      <p class="filename" v-for="file in files">{{ file.name }}</p>
    </div>
  </div>
</template>

<script lang="babel">
export default {
  props: {
    height: String,
    multiple: {
      type: Boolean,
      default(){
        return false;
      }
    },
    message: {
      type: String,
      default(){
        return "Click or drag to upload files";
      }
    }
  },
  data(){
    return {
      files: []
    }
  },
  methods: {
    getFiles(evt){
      let f = evt.target.files;
      for(let i = 0; i < f.length; i++){
        this.files.push(f[i]);
      }
    }
  }
}
</script>
