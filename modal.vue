<style scoped>
/*.modal{
  color: white;
  background-color: rgba(0, 0, 0, 0.5);
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}
.modal > .modal-wrapper{
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  width: 100%;
}
.modal > .modal-wrapper > .modal-content{
  width: 50%;
}*/
.modal{
  z-index:1;
  padding-top:100px;
  position:fixed;
  left:0;
  top:0;
  width:100%;
  height:100%;
  overflow:auto;
  background-color:rgb(0,0,0);
  background-color:rgba(0,0,0,0.4);
}
.modal-content{
  margin:auto;
  background-color:#fff;
  position:relative;
  padding:0;
  outline:0;
  width:600px
}
.modal-close{
  text-decoration: none;
  font-size: 20px;
  font-weight: bold;
  color: inherit;
  position: absolute;
  top: 0px;
  right: 7px;
}
.modal-close:hover,.modal-close:focus{
  color:#000;
  text-decoration:none;
  cursor:pointer
}
</style>

<template>
<div class="modal" v-show="!hidden" transition="fade">
  <div class="modal-content">
    <slot></slot>
    <span v-if="closeable" class="modal-close" @click="close()">&times;</span>
  </div>
</div>
</template>

<script lang="babel">
export default {
  props: {
    hidden: Boolean,
    closeable: Boolean,
  },
  methods: {
    close(){
      this.hidden = true;
    }
  }
}
</script>
