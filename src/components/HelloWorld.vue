<template lang="pug">
div
  div(v-for="worker in workers")
    div {{worker}}
</template>

<script>
import axios from 'axios'
  export default {
    name: 'HelloWorld',

    data(){
      return {
        workers: []
      }
    },
    mounted(){
      this.getWorkers()
    },
    methods:{
      getWorkers(){
        axios.post("http://localhost:8080/list")
        .then((data) => this.workers = data.data)
      }
    },

  }
</script>
