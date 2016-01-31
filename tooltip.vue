<style scoped>
.tooltip .tooltip-message {
  background: #1496bb;
  bottom: 100%;
  color: #fff;
  display: block;
  margin-bottom: 15px;
  opacity: 0;
  min-width: 90px;
  padding: 10px 0;
  text-align: center;
  position: absolute;
  transition: all .25s ease-out;
  box-shadow: 2px 2px 6px rgba(0, 0, 0, 0.28);
}

.tooltip .tooltip-message:after {
  border-left: solid transparent 10px;
  border-right: solid transparent 10px;
  border-top: solid #1496bb 10px;
  bottom: -10px;
  content: " ";
  height: 0;
  left: 50%;
  margin-left: -13px;
  position: absolute;
  width: 0;
}

.tooltip:hover .tooltip-message {
  opacity: 1;
  pointer-events: auto;
}
</style>

<template>
<span class="tooltip">
  <slot></slot>
  <span class="tooltip-message text tag" :style="{'min-width': width}">{{ text }}</span>
</span>
</template>

<script lang="babel">
export default {
  props: ["text", "width"]
}
</script>
