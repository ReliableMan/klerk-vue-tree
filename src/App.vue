<template>
 <div id="app">
  <TreeVue 
    :node="root"
    @changeFlag="moreRubrics"
  />
 </div>
</template>

<script>
import TreeVue from './components/TreeVue.vue';
import axios from 'axios';

export default {
  name: 'App',
  data () {
    return {
      root: []
    }
  },
  methods: {
    async fetchRubrics() {
      try {
        const response = await axios.get('https://www.klerk.ru/yindex.php/v3/event/rubrics');
        this.root = response.data
      } catch (e) {
        alert("Что-то пошло по плану")
      }
    }, 
    moreRubrics (boolean) {
     boolean ? this.fetchExtraRubrics() : this.fetchRubrics();
    }, 
    async fetchExtraRubrics () {
      try { 
        const response = await axios.get('https://www.klerk.ru/yindex.php/v3/event/rubrics?allowEmpty=1');
        this.root = response.data
      } catch (err) {
        console.error(err)
      }
    }
  },
  mounted () {
    this.fetchRubrics()
  },
  components: {
    TreeVue
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
