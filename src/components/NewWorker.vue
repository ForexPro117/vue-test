<template lang="pug">
div
    v-text-field(v-model="name" placeholder="ФИО")
    v-text-field(v-model="position" placeholder="Должность")
    v-btn(@click="addWorkers") Внести данные
</template>
    
<script>
import axios from "axios";
  export default {
    name: "NewWorker",
    
    data() {
    
    },
    methods: {
      addWorkers() {
        var name = this.name
        var position = this.position
        axios.post("http://localhost:8080/add", { name, position })
        .then(() => console.log("успех"));
      }
    },
  }
</script>
    