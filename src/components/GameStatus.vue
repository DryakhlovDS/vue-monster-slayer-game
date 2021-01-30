<template>
  <section class="card-status">
    <h3 v-if="isName">{{name}} won!</h3>
    <button @click="newGame"> Start new geme</button>
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
computed: {
  isName(){
    if (this.name) return true;
    return false;
  }
},
methods: {
  newGame(){
    this.$emit('newGame', true);
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