<template>
  <div>
    <h1>{{ msg }}</h1>
    <h2>{{msgfromfather}}</h2>
    <button v-on:click="onClickMe">click</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      msg: 'hello from componentA'
    }
  },
  props: ['msgfromfather'],
  methods: {
      onClickMe: function() {
          console.log(" 1");
          this.$emit("child-tell-me-something",this.msg);
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  font-weight: normal;
  color: #42b983;
}
</style>
