<style scoped>
  .component {
    line-height: 1.5em;
    margin: 0 auto;
    padding: 0 0 2em;
    overflow: hidden;
  }
  .tools > div {
    height: 60px;
    display: flex;
    align-items: center;
    justify-content: flex-end;
  }
  .tools .btn:not(:first-of-type) {
    margin-left: 5px;
  }
  table {
    border-collapse: collapse;
    margin-bottom: 3em;
    width: 100%;
    background: #fff;
  }
  td, th {
    padding: 0.75em 1.5em;
    text-align: left;
  }
  td.err {
    background-color: #e992b9;
    color: #fff;
    font-size: 0.75em;
    text-align: center;
    line-height: 1;
  }
  th {
    background-color: #FA8F44;
    font-weight: bold;
    color: #fff;
    white-space: nowrap;
    -webkit-user-select: none; /* webkit (safari, chrome) browsers */
    -moz-user-select: none; /* mozilla browsers */
    -khtml-user-select: none; /* webkit (konqueror) browsers */
    -ms-user-select: none; /* IE10+ */
  }
  tbody th {
    background-color: #2ea879;
  }
  tbody tr:nth-child(2n-1) {
    background-color: #f5f5f5;
    transition: all .125s ease-in-out;
  }
  tbody tr{
    height: 37px;
  }
  tbody tr:hover {
    background-color: rgba(129, 200, 208, 0.25);
    cursor: pointer;
  }

  tbody tr.active > td {
    background-color: rgba(129, 200, 208, 0.35);
  }
  .sticky-wrap {
    overflow: auto;
    position: relative;
    width: 100%;
    height: 30vh;
  }
  .sticky-wrap .sticky-thead,
  .sticky-wrap .sticky-col,
  .sticky-wrap .sticky-intersect {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 50;
    width: auto;
  }
  .sticky-wrap .sticky-thead {
    /*box-shadow: 0 0.25em 0.1em -0.1em rgba(0,0,0,.125);*/
    z-index: 100;
    width: 100%;
  }
  .sticky-wrap .sticky-intersect {
    display: block;
    z-index: 150;
  }
  .sticky-wrap .sticky-intersect th {
    background-color: #666;
    color: #eee;
  }
  .sticky-wrap td,
  .sticky-wrap th {
    box-sizing: border-box;
    cursor: pointer;
    position: relative;
  }
  .sticky-wrap td > span{
    position: absolute;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    left: 1.5em;
    right: 1.5em;
    top: 0.6em;
  }
  .arrow {
    display: inline-block;
    vertical-align: middle;
    width: 0;
    height: 0;
    margin-left: 5px;
    opacity: 0.66;
  }
  .arrow.asc {
    border-left: 4px solid transparent;
    border-right: 4px solid transparent;
    border-bottom: 4px solid #fff;
  }
  .arrow.dsc {
    border-left: 4px solid transparent;
    border-right: 4px solid transparent;
    border-top: 4px solid #fff;
  }
</style>

<template>
<div class="row tools">
  <div class="col-md-4">
    <input class="form-control" name="query" v-model="filterKey" placeholder="Search">
  </div>
  <div class="col-md-6 pull-right">
    <button class="btn btn-default" accesskey="a" @click="add()"><i class="fa fa-plus"></i> Add</button>
    <button class="btn btn-default" accesskey="c" @click="copy()"><i class="fa fa-clone"></i> Copy</button>
    <button class="btn btn-default" accesskey="d" @click="remove()"><i class="fa fa-trash"></i> Remove</button>
    <button class="btn btn-default" accesskey="x" @click="clear()"><i class="fa fa-trash"></i> Clear</button>
    <button class="btn btn-default" accesskey="p" @click="selectPrevious()"><i class="fa fa-angle-double-left"></i> Previous</button>
    <button class="btn btn-default" accesskey="n" @click="selectNext()"><i class="fa fa-angle-double-right"></i> Next</button>
    <button class="btn btn-default" accesskey="s" @click="save()"><i class="fa fa-save"></i> Save</button>
    <button class="btn btn-default" @click="submit()"><i class="fa fa-paper-plane"></i> Send</button>
  </div>
</div>
<section class="component">
  <div class="wrapper">
  <table v-el:datagrid>
    <thead>
      <tr class="header">
        <th v-for="key in columns"
          @click="sortBy(key)"
          :class="{active: sortKey == key}">
          {{key | capitalize}}
          <span class="arrow"
            :class="sortOrders[key] > 0 ? 'asc' : 'dsc'">
          </span>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="
        entry in data
        | filterBy filterKey
        | orderBy sortKey sortOrders[sortKey]"
        @click="setSelected(entry)"
        :class="{active: selected == entry}">
        <td v-for="key in columns"><span>{{ renderer[key] && renderer[key](entry[key], entry, key) || entry[key] }}</span></td>
      </tr>
    </tbody>
  </table>
  </div>
</section>
</template>

<script>
  import StickyHeader from '../js/stickyheader.js';

  export default {
    props: {
      data: Array,
      columns: Array,
      renderer: Object,
      selected: Object,
      filterKey: String
    },
    data: function(){
      var sortOrders = {};
      this.columns.forEach(function(key) {
        sortOrders[key] = 1
      });

      return {
        sortKey: '',
        focused: null,
        sortOrders: sortOrders
      }
    },
    created: function(){
      var savedData = localStorage.getItem('apn-piw');
      if(savedData){ this.data = JSON.parse(savedData) }
    },
    ready: function(){
      if(0 in this.data) this.setSelected(this.data[0]);
      else this.add();
      StickyHeader(this.$els.datagrid);
    },
    methods: {
      sortBy: function(key) {
        this.sortKey = key;
        this.sortOrders[key] = this.sortOrders[key] * -1;
      },
      clear: function(){
    		if(confirm("Do you really want to remove all rows?")){
    			for(var i = this.data.length - 1; i >= 0; i--){ this.remove(this.data[i]); }
    			this.add();
    		}
      },
      save: function(){
        localStorage.setItem('apn-piw', JSON.stringify(this.data));
      },
      setSelected: function(entry){
        this.$set('selected', entry);
        this.focused = 0;
        this.$dispatch('entry-selected', entry);
      },
      selectNext: function(){
        var index = this.data.indexOf(this.selected);
        if(index + 1 in this.data){
          this.setSelected(this.data[index + 1]);
        }
      },
      selectPrevious: function(){
        var index = this.data.indexOf(this.selected);
        if(index - 1 in this.data){
          this.setSelected(this.data[index - 1]);
        }
      },
      remove: function(){
        var index = this.data.indexOf(this.selected);

        if(index - 1 in this.data){
          this.setSelected(this.data[index - 1]);
        } else {
          this.setSelected(this.data[index + 1]);
        }

        this.data.splice(index, 1);
      },
      add: function(_entry){
        var entry = _entry || (function(cols){ var e = {}; cols.forEach(function(col){ e[col] = "" }); return e; })(this.columns);
        this.data.push(entry);
        this.setSelected(entry);
        this.$dispatch('entry-added', entry);
      },
      copy: function(){
        this.add(JSON.parse(JSON.stringify(this.selected)));
      }
    }
  }
</script>
