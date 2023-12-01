<template>
    <div :style="{
        top: vehicle.y + 'px',
        left: vehicle.x + 'px',
        position: 'absolute', 
    }">
    <img src="./paper.svg"  :style="{
        transform: 'rotate(' + (vehicle.angle + 90) + 'deg)',
    }" />
    <h2>
        {{ vehicle.name }}
    </h2>
    </div>
  </template>
  
  <script setup lang="ts">
import type { Player } from '@/logic/gameService';
import type { PropType } from 'vue';


  const props = defineProps({
    vehicle: {type : Object as PropType<Player>,
    required: true,
    },
    })
  </script>


  

  