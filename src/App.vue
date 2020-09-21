<template>
  <div id="app">
    <RandomValue :value="tree.value" :tree="tree" :validate="validate"></RandomValue>
  </div>
</template>

<script>
import axios from 'axios'
import RandomValue from '@/components/RandomValue.vue'

export default {
  name: 'App',
  components: {
    RandomValue
  },
  data() {
    return {
      tree: {}
    }
  },
  methods: {
    async getTree() {
      const quantity = 6
      const response = await axios.get(`http://localhost:4251/api/tree?quantity=${quantity}`)
      this.tree = JSON.parse(response.data)
    },
    validate(value) {
      console.log(value)
    }
  },
  mounted() {
    this.getTree()
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
