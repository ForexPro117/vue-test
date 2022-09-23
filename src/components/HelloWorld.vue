<template lang="pug">
div
  v-data-table.mt-10.table(:headers="headers" :items="workers" style="width:1000px")
    template(v-slot:item.actions="{ item }")
      v-icon(small @click="editWorker(item)") mdi-pencil
      v-icon(small @click="deleteWorker(item)") mdi-delete

  v-dialog(v-model="deleteDialog" width="800")
    v-card
      v-card-title(class="text-h5") Вы уверены, что хотите удалить данные об этом работнике?
      v-divider
      v-card-actions 
        v-btn( color="red" text @click="closeDeleteDialog()") отмена
          v-icon(right) mdi-close
        v-spacer
        v-btn( color="teal accent-4" text @click="deleteWorkerCofirm()") удалить
          v-icon(right) mdi-delete


  v-dialog(v-model="editDialog" width="500")
    v-card
      v-card-title(class="text-h5") Изменение данных работника
      v-card-text ФИО
        v-text-field(v-model="name")
      v-card-text Должность
        v-text-field(v-model="position")
      v-divider
      v-card-actions
        v-btn( color="red" text @click="closeEditDialog()") отмена
          v-icon(right) mdi-close
        v-spacer
        v-btn( color="teal accent-4" text @click="editWorkerConfirm()") изменить
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
        deleteDialog:false,
        editDialog:false,
        deleteUUID:-1,
        uuid: '',
        name: '',
        position: '',
        workers: [],
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
      deleteWorkerCofirm(){
        axios.delete(`http://localhost:8080/delete/${this.deleteUUID}`)
        .then(() => this.closeDeleteDialog())
      },
      closeDeleteDialog(){
        this.deleteDialog = false
        this.getWorkers()
        this.deleteUUID = -1
      },
      deleteWorker(item){
        this.deleteUUID = item.uuid
        this.deleteDialog = true
      },
      editWorker(item){
        this.uuid = item.uuid
        this.name = item.name
        this.position = item.position
        this.editDialog = true
      },
      editWorkerConfirm(){
        axios.post('http://localhost:8080/edit', { uuid: this.uuid, name: this.name, position: this.position })
        .then(() => this.closeEditDialog())
      },
      closeEditDialog(){
        this.editDialog = false
        this.getWorkers()
        this.uuid = ''
        this.name = ''
        this.position = ''
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