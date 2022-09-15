<template lang="pug">
  div
    v-text-field(v-model="name" placeholder="ФИО")
    v-text-field(v-model="position" placeholder="Должность")
    v-btn(@click="addWorker") Внести данные
</template>

<script>
import axios from 'axios'
export default {
  name: 'NewWorker',

  data() {
    return {
      name: '',
      position: '',
    }
  },
  methods: {
    addWorker() {
      axios
        .post('http://localhost:8080/add', { name: this.name, position: this.position })
        .then(() => console.log('успех'))
    },
  },
}
</script>
