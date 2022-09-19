<template lang="pug">
div
  v-data-table(:headers="headers" :items="workers")
    <!-- template(v-slot:item.actions="{ item }")
      v-icon(small @click="editWorker(item)")
        | mdi-pencil
      v-icon(small @click="deleteWorker(item)")
        | mdi-delete -->
</template>

<script>
import axios from 'axios'
  export default {
    name: 'HelloWorld',

    data(){
      return {
        headers: [
          { text: 'ФИО', align: 'start', value: 'name' },
          { text: 'Должность', value: 'position' },
          { text: 'Действия', value: 'action', sortable: false }
        ],
        workers: []
      }
    },
    mounted(){
      this.getWorkers()
      
    },
    methods:{
      getWorkers(){
        axios.get("http://localhost:8080/get")
        .then((data) => { this.workers = data.data })
      },
      deleteWorker(item){
        axios.delete(`http://localhost:8080/delete/${this.workers[this.workers.indexOf(item)]}`)
        .then(() => this.getWorkers())
      },
      editWorker(){
        axios.post('http://localhost:8080/edit', { uuid: this.uuid, name: this.name, position: this.position })
        .then(() => this.getWorkers())
      }
    },

  }
</script>
