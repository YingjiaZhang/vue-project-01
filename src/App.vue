<template>
  <div id="app">
     <h1>{{title}}</h1>
     <h1 v-text="title"></h1>
     <h1 v-html="title"></h1>
     <input v-model="newItem" v-on:keyup.enter="addItem"/>
     <ul>
        <li v-for="item in items" v-bind:class="{finished:item.isFinished}" v-on:click="toggleFinished(item)" >{{item.label}}</li>
     </ul>
     <component-a msgfromfather="form app.vue" v-on:child-tell-me-something="listenToMyBoy"></component-a>
     <p>this is from child : {{childWords}}</p>


  </div>
</template>

<script>
import Store from './store'
import ComponentA from './components/componentA'  // import other components
export default {
  name: 'app',
  data () {
     return {
       title: 'This is to list<span>??</span>',
       items: Store.fetch(),
       newItem: '',
       childWords: ''
     }
   },
  components: {ComponentA},
  methods: {
     toggleFinished: function(item) {
       item.isFinished = !item.isFinished;
     },
     addItem: function(){
       this.items.push({
         label: this.newItem,
         isFinished: false
       });
       this.newItem = '';
     },
    listenToMyBoy: function(msg){
      console.log(" 2");
      this.childWords = msg;
    }
  },
  watch: {
     items: {
        handler: function (items) {
          Store.save(items)
        },
        deep: true
     }
  }
}
</script>

<style>
.finished{
  text-decoration: underline;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
