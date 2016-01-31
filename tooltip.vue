<style scoped>
.tooltip .text{
  display:none;
}

.tooltip:hover .text{
  display:inline-block;
  background: #1496bb;
  bottom: 100%;
  color: #fff;
  margin-bottom: 15px;
  min-width: 90px;
  padding: 10px 0;
  text-align: center;
  position: absolute;
  transition: all .25s ease-out;
  box-shadow: 2px 2px 6px rgba(0, 0, 0, 0.28);
}

.tooltip .text:after {
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
</style>

<template>
<span class="tooltip">
  <slot></slot>
  <span class="text tag" :style="{'min-width': width}">{{ text }}</span>
</span>
</template>

<script lang="babel">
export default {
  props: ["text", "width"]
}
</script>
