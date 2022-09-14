<template lang="pug">
  div
    h1 Ты дома епт!
    v-btn( @click="getWorkers") dd
    div(v-for='worker,key in workers')
      div {{key}} - {{worker}} 
</template>

<script>
import axios from 'axios'

  export default {
    name: 'HelloWorld',

    data(){
      return {
        workers:[]
      }
    },
    mounted(){
  },
    methods:{
      
      addWorkers(){
        axios.post("http://localhost:8080/adds",{name:"artem"})
        .then(()=> console.log("успех"))
      },
      getWorkers(){
        axios.post("http://localhost:8080/sdf")
        .then((response)=>  this.workers=response.data)
      }
    },
  }
</script>
