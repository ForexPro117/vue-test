<template lang="pug">
div
  div.mt-5(v-for="worker in workers")
    div имя: {{worker.name}} должность: {{worker.position}} код: {{worker.uuid}} 
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
        axios.get("http://localhost:8080/get")
        .then((data) => {
          this.workers = data.data
          this.getWorker()
        })
      },
      getWorker(){
        axios.get(`http://localhost:8080/get/${this.workers[0].uuid}`)
        .then((data) => {
          console.log("you first worker", data.data);
        })
      }
    },

  }
</script>
