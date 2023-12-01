<template>
    <div v-for="player in board?.players" :key="player.name">
        <Vehicle :vehicle="player" />
    </div>
    <VehicleControl v-if="playerid" :playerid="playerid" />
    <RegisterVue @register="handleRegister"/>
</template>

<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue';
import RegisterVue from './Register.vue';
import { getBoard, type Board } from '@/logic/gameService';
import Vehicle from './Vehicle.vue';
import VehicleControl from './VehicleControl.vue';

const playerid = ref<number | null>(null);
const board = ref<Board | null>(null);

const handleRegister = (id: number) => {
    playerid.value = id;
};

const fetchBoards = async () => {
   board.value = await getBoard();
}

let interval: number | null = null;

onMounted(() => {
    interval = setInterval(fetchBoards, 100);
});

onUnmounted(() => {
    if (interval) {
        clearInterval(interval);
    }
});

</script>