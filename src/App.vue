<template lang="pug">
  v-app
    v-container
      header
        router-link.none-decor(to="/") 
          v-btn Список рабочих
        router-link.hne.none-decor(to="/about") 
          v-btn Добавить рабочего
      v-main
        router-view
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    //
  }),
};
</script>
<style scoped>
.none-decor{
  text-decoration: none;
}
</style>
<style>
*{
  font-family: Roboto;
}
.hne{
  margin-left: 20px;
}
</style>