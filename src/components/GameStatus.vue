<template>
  <section class="card-status">
    <NewGame v-if="!setSettings" @newSettings="newSettings" />
    <Settings v-else />
  </section>
</template>

<script>
import NewGame from './NewGame.vue';
import Settings from './Settings.vue';

export default {
name: "GameStatus",
components: {
  NewGame,
  Settings,
},
data: () => ({
  setSettings: false,
}),
methods: {
  newSettings(value){
    this.setSettings = value;
  },
}
}
</script>

<style lang="scss" scoped>
.card-status{
  width: 96%;
  max-width: 600px;
  margin: 2rem auto;
  padding: 1rem;
  border-radius: var(--border-radius);
  border: 1px solid var(--color-shadow);
  background-color: var(--color-bg);
  color: var(--color-red);

  
}
</style>