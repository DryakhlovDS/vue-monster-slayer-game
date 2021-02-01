<template>
  <div class="settings">
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
        @click="newGame('normal', newName)"
        class="settings__btn"
        :disabled="!newName"
        >normal</button>
      <button 
        @click="newGame('hard', newName)"
        class="settings__btn" 
        :disabled="!newName"
        >hard</button>
    </div>
</template>

<script>
export default {
  name: "Settings",
  data: () =>({
    newName: "",
  }),
  inject: ['newGame'],
  computed: {
    emptyName(){
      if (this.newName) return "";
      return "settings__input-empty";
    }
  },
}
</script>

<style lang="scss" scoped>
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