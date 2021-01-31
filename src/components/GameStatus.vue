<template>
  <section class="card-status">
    <!-- <div v-if="!setSettings" class="new-game">
      <h3 v-if="isName" class="new-game__title">{{name}} won!</h3>
      <button @click="newSettings" class="new-game__btn">
        <div class="border-left"></div>
        <div class="border-top"></div>
        <div class="border-right"></div>
        <div class="border-bottom"></div>
         Start new geme</button>
    </div>
    <div v-else class="settings">
      <label for="name">Name player :</label>
      <input 
        v-model="newName" 
        type="text" 
        id="name" 
        class="settings__input" 
        :class="emptyName"
        placeholder="Enter your name">
      <br>
      <button
        @click="newGame('normal')"
        class="settings__btn"
        :disabled="!newName"
        >normal</button>
      <button 
        @click="newGame('hard')"
        class="settings__btn" 
        :disabled="!newName"
        >hard</button>
    </div> -->
    <component :is="setSettings" @newSettings="newSettings"></component>
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
props: {
  name: {
    type: String,
    default: "",
  }
},
data: () => ({
  newName: "",
  setSettings: "NewGame",
}),
computed: {
  isName(){
    if (this.name) return true;
    return false;
  },
  emptyName(){
    if (this.newName) return "";
    return "settings__input-empty";
  }
},
methods: {
  newGame(type){
    this.$emit('newGame', type, this.newName);
  },
  newSettings(cmp){
    this.setSettings = cmp;
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

.settings{
  padding: 0.5rem;

  & label{
    font-size: 1.3rem;
    font-weight: 700;
  }

  &__input{
    margin-left: 1rem;
    padding-left: 0.5rem;
    width: 60%;
    height: 2.5rem;
    font-size: 1.3rem;
    border: none;
    border-bottom: 2px solid var(--color-card);
    color: var(--color-red);
    background-color: var(--color-bg);

    &::placeholder{
      color: var(--color-text);
    }

    &:focus{
      outline: none;
    }

    &-empty{
      border-color: var(--color-red);
      // border-bottom: 2px solid  var(--color-red);
    }
  }

  &__btn{
    margin-top: 1rem;
    padding: 1rem;
    width: 90%;
    max-width: calc(400px - 4rem);
    font-size: 1.3rem;
    color: var(--color-text);
    background-color: var(--color-bg);
    border: 2px solid var(--color-shadow);
    border-radius: 1rem;
    cursor: pointer;
    text-transform: uppercase;
    transition: all 0.2s linear;

    &:disabled{
      color: var(--color-shadow);
      border-color: var(--color-card);
      // background-color: var(--color-card);
      cursor: default;

      &:hover{
        color: var(--color-shadow);
        box-shadow: none;
      }
    }

    &:hover{
      color: var(--color-red);
      box-shadow: 0 0 12px var(--color-shadow);
    }
  }  
}
</style>