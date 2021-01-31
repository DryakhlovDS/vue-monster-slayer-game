<template>
  <div class="new-game">
      <h3 v-if="isName" class="new-game__title">{{name}} won!</h3>
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
  },
  },
  methods: {
    newSettings(){
      this.$emit('newSettings', "Settings");
    },
  },
}
</script>

<style lang="scss" scoped>

</style>