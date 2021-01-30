<template>
  <section class="actions">
    <button class="actions__btn" @click="atack">Attack</button>
    <button class="actions__btn" @click="sAtack">Special ttack</button>
    <button class="actions__btn" @click="heal">Heal</button>
    <button class="actions__btn" @click="flag">White flag</button>
  </section>
</template>

<script>
export default {
  name:"Actions",
  methods: {
    atack() {
      this.$emit("atack");
    },
    sAtack() {
      this.$emit("sAtack");
      },
    heal() {
      this.$emit("heal");
      },
    flag() {
      this.$emit("flag");
      }
  }

}
</script>

<style lang="scss" scoped>
.actions{
  display: flex;
  flex-direction: column;
  width: 100%;
  max-width: 400px;
  margin: 1rem auto;
  padding: 1rem 2rem;

  &__btn{
    padding: 1rem;
    font-size: 1.3rem;
    &+&{
      margin-top: 0.5rem;
    }
  }
}
</style>