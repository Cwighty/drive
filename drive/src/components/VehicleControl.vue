<script setup lang="ts">
import { onMounted, onUnmounted, ref, watch } from 'vue';
import { move } from '@/logic/gameService';

const props = defineProps({
  playerid: Number
});

const controlKeys = {
  forwards: "w",
  backwards: "s",
  left: "a",
  right: "d",
};

const keydownListener = async (event: KeyboardEvent) => {
  if (!props.playerid) return;

  if (event.key === controlKeys.forwards) await move(props.playerid, "Forward");
  if (event.key === controlKeys.backwards) await move(props.playerid, "Backward");
  if (event.key === controlKeys.left) await move(props.playerid, "Left");
  if (event.key === controlKeys.right) await move(props.playerid, "Right");
};

const keyupListener = async (event: KeyboardEvent) => {
  if (!props.playerid) return;

  if (event.key === controlKeys.forwards) await move(props.playerid, "StopForward");
  if (event.key === controlKeys.backwards) await move(props.playerid, "StopBackward");
  if (event.key === controlKeys.left) await move(props.playerid, "StopLeft");
  if (event.key === controlKeys.right) await move(props.playerid, "StopRight");
};

onMounted(() => {
  window.addEventListener("keydown", keydownListener);
  window.addEventListener("keyup", keyupListener);
});

onUnmounted(() => {
  window.removeEventListener("keydown", keydownListener);
  window.removeEventListener("keyup", keyupListener);
});
</script>
