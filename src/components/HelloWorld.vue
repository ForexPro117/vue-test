<template lang="pug">
div
  v-text-field(v-model="uuid" placeholder="Введите UUID рабочего, которого необходимо удалить") 
  v-btn(@click="deleteWorker") Удалить рабочего

  div.mt-5(v-for="worker in workers")
    div имя: {{worker.name}} должность: {{worker.position}} код: {{worker.uuid}} 
</template>

<script>
import axios from 'axios'
  export default {
    name: 'HelloWorld',

    data(){
      return {
        workers: [],
        uuid: '',
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
        })
      },
      deleteWorker(){
        axios.get(`http://localhost:8080/delete/${this.uuid}`)
        .then(() => console.log("успех")),
        this.getWorkers()
      }
    },

  }
</script>
