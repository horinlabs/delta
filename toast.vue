<style scoped>
.toast{
  position: fixed;
  min-width: 200px;
  min-height: 50px;
}
</style>

<template>
<div class="toast" :style="toastStyle">
  <alert
    :icon="alert.icon"
    :message="alert.message"
    :time="alert.time || 0"
    v-for="alert in alerts"
    @alert-hidden.stop="removeToast(alert)">
  </alert>
</div>
</template>

<script lang="babel">
import Alert from './alert'

export default {
  props: {
    alerts: Array,
    position: {
      type: String,
      default(){
        return 'top right';
      }
    }
  },
  computed: {
    toastStyle(){
      let toastStyle = {};
      this.position.split(' ').forEach((pos) => toastStyle[pos] = '15px');
      return toastStyle;
    }
  },
  methods: {
    removeToast(alert){
      this.$nextTick(() => {
        let index = this.alerts.indexOf(alert);
        this.alerts.splice(index);
      });
    }
  },
  components: {
      Alert
  }
}
</script>
