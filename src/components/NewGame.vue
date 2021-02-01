<template>
  <div class="new-game">
      <h3 v-if="isName" class="new-game__title">{{winnerName}} won!</h3>
      <button @click="newSettings" class="new-game__btn">
        <div class="border-left"></div>
        <div class="border-top"></div>
        <div class="border-right"></div>
        <div class="border-bottom"></div>
         Start new geme</button>
    </div>
</template>

<script>
export default {
  name: "NewGame",
  inject: ['winner'],
  computed: {
    isName(){
      if (this.winnerName) return true;
      return false;
    },
    winnerName() {
      return this.winner();
    }
  },
  methods: {
    newSettings(){
      this.$emit('newSettings', 'Settings');
    },
  },
}
</script>

<style lang="scss" scoped>
.new-game{
  padding: 1rem;
  &__title{
    font-size: 1.2rem;
    margin-bottom: 1rem;
  }

  &__btn{
    position: relative;
    padding: 1rem;
    font-size: 1.3rem;
    color: var(--color-red);
    background-color: var(--color-bg);
    border: none;
    // border: 2px solid var(--color-shadow);
    border-radius: 1rem;
    cursor: pointer;
    overflow: hidden;
    
    &:hover{
      & .border-left,
      .border-right{
        transform: translateY(0);
      }
      & .border-top,
      .border-bottom{
        transform: translateX(0);
      }
    }
  }

  & .border{

    &-left,
    &-top,
    &-right,
    &-bottom{
      position: absolute;
      background-color: var(--color-text);
      transition: transform 0.3s linear;
    }

    &-left{
      height: 100%;
      width: 2px;
      left: 0;
      top: 0;
      transform: translateY(100%);
    }
    &-top{
      height: 2px;
      width: 100%;
      left: 0;
      top: 0;
      transform: translateX(-100%);
    }
    &-right{
      height: 100%;
      width: 2px;
      right: 0;
      top: 0;
      transform: translateY(-100%);
    }
    &-bottom{
      height: 2px;
      width: 100%;
      left: 0;
      bottom: 0;
      transform: translateX(100%);
    }
  }
}
</style>