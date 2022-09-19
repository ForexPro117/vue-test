<template lang="pug">
div
  v-data-table.mt-10.table(:headers="headers" :items="workers" style="width:1000px")
    template(v-slot:item.actions="{ item }")
      v-icon(small @click="dialog=true") mdi-pencil
      v-icon(small @click="deleteWorker(item)") mdi-delete




  v-dialog(v-model="dialog" width="500")
    v-card
      v-card-title За шо менять
      v-card-text Тут ты типо выводишт свой обект по частям, т.е. тебе над передавать объектики
      v-divider
      v-card-actions
        v-btn( color="red" text @click="dialog=false") отмена
        v-spacer
        v-btn( color="teal accent-4" text) изменить
          v-icon(right) mdi-pencil     
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
          { text: 'Действия', value: 'actions', sortable: false }
        ],
        dialog:false,
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
<style scoped>
.table{
  border: 1px solid #ccc;
  box-shadow: 4px 4px 8px 0px rgba(34, 60, 80, 0.2);
}
</style>