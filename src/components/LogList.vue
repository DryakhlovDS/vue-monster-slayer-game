<template>
  <section class="logs">
    <h4 class="logs__title">Battle logs:</h4>
    <ul>
      <li v-for="(log, index) of logs" :key="index" class="logs__item">{{log}}</li>
    </ul>
  </section>
</template>

<script>
export default {
  name: "LogList",
  props: {
    logs:{
      type: Array,
      default: () =>([]),
    }
  }
}
</script>

<style lang="scss" scoped>
.logs{
  width: 100%;
  max-width: 400px;
  margin: 2rem auto;
  padding: 1rem;
  border-radius: 0.5rem;
  border: 1px solid #000000 ;
  
  &__title{
    // text-transform: capitalize;
    margin-bottom: 0.5rem;
  }

  & ul{
    list-style: none;
  }

  &__item{
    &+&{
      margin-top: 0.5rem;
    }
  }
}
</style>