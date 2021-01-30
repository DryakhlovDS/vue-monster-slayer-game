<template>
  <section class="actions">
    <button class="actions__btn" @click="atack">
      <img src="../assets/sword.png" class="actions__icon"/>Attack</button>
    <button class="actions__btn" @click="sAtack" :disabled="!superAtackEnable">
      <img src="../assets/swords.png" class="actions__icon"/> Special atack</button>
    <button class="actions__btn" @click="heal">
      <img src="../assets/healing.png" class="actions__icon"/>Heal</button>
    <button class="actions__btn" @click="flag">
      <img src="../assets/flag-hand-drawn-outline.svg" class="actions__icon"/>White flag</button>
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
    padding: 0.5rem;
    font-size: 1.3rem;
    color: var(--color-red);;
    background-color: var(--color-card);
    border: 2px solid var(--color-shadow);
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;

    &:disabled{
      color: var(--color-shadow);
      border-color: var(--color-card);
      background-color: var(--color-bg);
      cursor: default;
    }

    &+&{
      margin-top: 0.5rem;
    }

    &:hover{
      & .actions__icon{
        animation: action 1s infinite;
        // transform: rotate(-15deg);
        // transform: scale(1.1, 1.1);
      }
    }
  }

  &__icon{
    height: 35px;
    margin-right: 1rem;
  }
}

@keyframes action {
  from{
    transform: rotate(0);
  }
  25%{
    transform: rotate(-5deg);
  }
  50%{
    transform: rotate(0);
  }
  75%{
    transform: rotate(5deg);
  }
  to{
    transform: rotate(0);
  }
}
</style>