<template>
  <div id="app">
    <h1 v-html="title">{{title}}</h1>
    <input v-model="newItem" @keyup.enter="addNew">
    <ul>
      <li v-for="item in items" :class="{finished:item.isFinished}" @click="toggleFinish(item)">
        {{item.label}}
      </li>
    </ul>
    <p>child tells me:{{childWords}}</p>
    <component-a msgfromfather='you die!' @child-tell-me-something="listenToMyBoy"></component-a>
    <!-- <img src="./assets/logo.png"> -->
    <router-view></router-view>
  </div>
</template>

<script>
import Store from './store'
import ComponentA from './components/ComponentA'
export default {
  data () {
    return {
      title: 'this is todo list',
      items: Store.fetch(),
      newItem: '',
      childWords:''
    }
  },
  components: {ComponentA},
  watch: {
    items: {
      handler: function(items){
        Store.save(items)
      },
      deep:true
    }
  },
  events: {
    'child-tell-me-something':function(msg){
      this.childWords = msg;
    }
  },
  methods: {
    toggleFinish: function (item) {
      console.log(item.isFinished=!item.isFinished)
    },
    addNew: function(){
      this.items.push({
        label: this.newItem,
        isFinished: false
      })
      this.newItem = ''
    },
    listenToMyBoy(msg){
      //console.log(msg);
      this.childWords=msg
    }
  }
}
</script>

<style>
.finished{text-decoration: underline;}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
