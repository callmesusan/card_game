<template>
  <h1>Details</h1>
  <div id="spacer"></div>
  <h3>- {{ player.realName }}</h3>
  <h3>- {{ player.playerName }}</h3>
  <h3>- {{ player.asset }}</h3>
</template>

<script lang="ts">
import { ref, PropType, defineComponent } from "vue";
import PlayerModel from "../interfaces/PlayerInterface.vue";

export default defineComponent({
  name: "DetailView",
  props: {
    player: {
      type: Object as PropType<PlayerModel>,
      required: true,
    },
  },
});
</script>

<style>
</style>