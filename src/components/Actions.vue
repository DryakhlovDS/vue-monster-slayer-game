<template>
  <section class="actions">
    <button class="actions__btn" @click="atack">Attack</button>
    <button class="actions__btn" @click="sAtack" :disabled="!superAtackEnable">Special atack</button>
    <button class="actions__btn" @click="heal">Heal</button>
    <button class="actions__btn" @click="flag">White flag</button>
  </section>
</template>

<script>
export default {
  name:"Actions",
  data: () => ({
    sp: 3,
  }),
  computed: {
    superAtackEnable(){
      return this.sp === 3;
    },
  },
  methods: {
    atack() {
      this.spInc();
      this.$emit("atack");
    },
    sAtack() {
      this.sp = 0;
      this.$emit("sAtack");
      },
    heal() {
      this.spInc();
      this.$emit("heal");
      },
    flag() {
      this.$emit("flag");
      },
    spInc(){
      if (this.sp < 3) this.sp++;
    },
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