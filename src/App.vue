<template>
  <div>
    <PhoneList />
  </div>
</template>

<script>
import PhoneList from './components/PhoneList.vue';

export default {
  components: { PhoneList }
}
</script>

<style scoped>
.welcome-heading {
  background-color: black;
  color: white;
  font-family: Cambria, 'Times New Roman', Times, serif;
  text-align: center;
  padding: 20px;
}
</style>
