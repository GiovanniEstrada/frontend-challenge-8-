<script setup lang="ts">

import {ref} from 'vue'

const count = ref(0)

function counter() {
  count.value++;
  console.log(count);
}

defineProps<{
  msg: string
}>()

</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }} {{count}}</h1>
    <button @click="counter" >Touch It</button>
    <h3>
      You’ve successfully created a project with Vue
    </h3>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
