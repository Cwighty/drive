<template>
  <div>
    <input type="text" v-model="name" />
    <button @click="registerPlayer">Register</button>
  </div>
</template>

<script setup lang="ts">

import { ref } from 'vue';
import { register } from '@/logic/gameService';

const name = ref('');

const emit = defineEmits(['register']);

const registerPlayer = async () => {
  const playerid = await register(name.value);
  emit('register', playerid);
};

</script>

  <style scoped>
  div {
    /* center the div */
    position: absolute;
    top: 40%;
    left: 45%;

  }
  </style>