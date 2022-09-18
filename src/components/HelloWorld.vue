<template lang="pug">
div
  v-text-field(v-model="uuid" placeholder="Введите UUID рабочего") 
  v-text-field(v-model="name" placeholder="ФИО") 
  v-text-field(v-model="position" placeholder="Должность") 
  v-btn(@click="editWorker") Изменить
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
        name: '',
        position: ''
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
        axios.delete(`http://localhost:8080/delete/${this.uuid}`)
        .then(() => console.log("успех"))
      },
      editWorker(){
        axios
        .post('http://localhost:8080/edit', { uuid: this.uuid, name: this.name, position: this.position })
        .then(() => console.log('успех'))
      }
    },

  }
</script>
