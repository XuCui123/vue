<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1>{{msgfromfather}}</h1>
    <button v-on:click="onClickMe">Click!</button>
    <button v-on:click="onClickMouse">open mouse!</button>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to componentA'
    }
  },
  props:['msgfromfather'],
  events: {
    'onAddNew': function(items){
      console.log(items)
    }
  },
  methods:{
    onClickMe() {
      console.log(this.msgfromfather)
    },
    onClickMouse() {
      // this.$emit('child-tell-me-something',this.msg);
      this.$dispatch('child-tell-me-something',this.msg);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
