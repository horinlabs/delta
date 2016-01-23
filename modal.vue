<style scoped>

</style>

<template>
<div v-ref="modal" class="modal fade">
  <div class="modal-dialog" transition="fade">
    <div class="modal-content">
      <div class="modal-header">
        {{ title }}
      </div>
      <div class="modal-body">
        <slot></slot>
      </div>
      <div class="modal-footer">
        <button v-for="button in buttons" class="btn btn-success" @click="button.click()"><i class="fa" :class="{{button.className}}"></i> {{button.name}}</button>
      </div>
    </div>
  </div>
</div>
</template>

<script lang="babel">
export default {
  props: {
    title: String,
    modal: Boolean,
    buttons: Array
  },
  data() {

  },
  close(){
    this.$els.modal.style.display = "none";
  },
  components: {

  }
}
</script>
