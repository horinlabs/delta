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
</style>

<template>
<div class="modal" transition="fade">
  <div class="modal-content">
    <slot></slot>
  </div>
</div>
</template>

<script lang="babel">
export default {
  props: {
  },
  data() {

  },
  close(){
  }
}
</script>
