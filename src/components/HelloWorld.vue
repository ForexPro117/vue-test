<template lang="pug">
  h1 Ты дома епт!
</template>

<script>
import axios from 'axios'
  export default {
    name: 'HelloWorld',

    data(){
      return {

      }
    },
    methods:{
      addWorkers(){
        axios.get("http://localhost:8080/add",{name:"worker",position:"prorab"})
        .then(()=> console.log("успех"))
      }
    },
  }
</script>
