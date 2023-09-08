<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})


const count = ref(0)
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
  </div>
</template>

<style scoped>
.pic1{
    height: 2000px;
    width: 200px;
}
.pic2{
    height: 2000px;
    width: 200px;
}
</style>
