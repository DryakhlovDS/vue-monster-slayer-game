<template>
  <section class="card-status">
    <div v-if="!setSettings" class="new-game">
      <h3 v-if="isName">{{name}} won!</h3>
      <button @click="newSettings"> Start new geme</button>
    </div>
    <div v-else class="settings">
      <label for="name">Name player:</label>
      <input v-model="newName" type="text" id="name">
      <br>
      <button @click="newGame('normal')">normal</button>
      <button @click="newGame('hard')">hard</button>
    </div>
  </section>
</template>

<script>
export default {
name: "GameStatus",
props: {
  name: {
    type: String,
    default: "",
  }
},
data: () => ({
  newName: "",
  setSettings: false,
}),
computed: {
  isName(){
    if (this.name) return true;
    return false;
  }
},
methods: {
  newGame(type){
    this.$emit('newGame', type, this.newName);
  },
  newSettings(){
    this.setSettings = true;
  },
}
}
</script>

<style lang="scss" scoped>
.card-status{
width: 100%;
  max-width: 600px;
  margin: 2rem auto;
  padding: 1rem;
  border-radius: 20px;
  border: 1px solid #000000;
}
</style>