<template>
  <div class="player">
    <h4 class="player__title">{{name}} health</h4>
    <div class="player__health-bar">
      <div class="player__health" :style="healthWidth"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "PlayerBar",
  props: {
    name : {
      type: String,
      default: "",
    },
    health: {
      type: Number,
      default: 0,
    }
  },
  computed: {
    healthWidth(){
      if (this.health < 0 )
      {
        return `width: 0%`
      }
      return `width: ${this.health}%`
    },
  },

}
</script>

<style lang="scss" scoped>
.player{
  width: 100%;
  max-width: 600px;
  padding: 1rem 1.5rem;
  border: 2px solid #000000;

  &__title{
    margin-bottom: 0.7rem;
  }

  &__health
  {
    height: inherit;
    background-color: green;
    transition: width 0.7s ease-out;
    
    &-bar {
    width: 100%;
    height: 2rem;
    background-color: #00000030;
    }
  }

}
</style>