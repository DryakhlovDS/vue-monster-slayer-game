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
        @click="newGame('normal')"
        class="settings__btn"
        :disabled="!newName"
        >normal</button>
      <button 
        @click="newGame('hard')"
        class="settings__btn" 
        :disabled="!newName"
        >hard</button>
    </div>
</template>