<style scoped>
.topnav{padding:8px 8px}
.topnav a,.sidenav a,.dropnav a,.dropdown-content a{text-decoration:none !important}
.topnav a{padding:0 8px;border-bottom:3px solid transparent;-webkit-transition:all 0.3s ease;transition:all 0.3s ease}
.topnav a:hover{border-bottom:3px solid #fff}
.topnav .dropdown-hover a{border-bottom:0}
.opennav,.closenav{color:inherit}
.opennav:hover,.closenav:hover{cursor:pointer;opacity:0.8}
.sidenav{height:100%;width:200px;background-color:#fff;position:fixed !important;z-index:1;overflow:auto}
.sidenav a{padding:4px 2px 4px 16px}
.sidenav a:hover,.sidenav a:focus{background-color:#ccc}
.sidenav a,.dropnav a{display:block;transition:.3s}
.dropnav {background-color:#fff}
.dropnav a:hover{text-decoration:underline !important}
</style>

<template>
  <header class="container">
    <span class="w3-opennav w3-xlarge" @click="open()">&#9776;</span>
    <nav class="sidenav" v-show="hidden">
      <a href="#" @click="close()" class="closenav large">Close &times;</a>
      <ul>
        <li v-for="item in items">
          <a :href="item.url"><i :class="item.icon"></i> {{ item.text }}</a>
          <ul class="dropdown" v-if="item.children">
            <li v-for="child in item.children">
              <a :href="child.url">{{ child.text }}</a>
            </li>
          </ul>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script lang="babel">
export default {
  props: {
    items: Array
  },
  data(){
    return {
      hidden: true
    }
  },
  methods: {
    open(){
      this.hidden = false;
    },
    close(){
      this.hidden = true;
    }
  }
}
</script>
