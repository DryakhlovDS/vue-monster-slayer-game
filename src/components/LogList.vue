<template>
  <section class="logs">
    <h4 class="logs__title">Battle logs:</h4>
    <ul>
      <li v-for="(log, index) of logs" :key="index" class="logs__item">{{log.player}} {{log.action}} {{log.value}}</li>
    </ul>
  </section>
</template>

<script>
export default {
  name: "LogList",
  props: {
    logs: {
      type: Array,
      default: () => ([]),
    }
  }
}
</script>

<style lang="scss" scoped>
.logs{
  width: 90%;
  max-width: 400px;
  margin: 2rem auto;
  padding: 1rem;
  border-radius: var(--border-radius);
  border: 1px solid var(--color-card) ;
  box-shadow: 0 2px 13px var(--color-shadow);

  
  &__title{
    position: relative;
    // text-transform: capitalize;
    margin-bottom: 1.5rem;

    &::after{
      content: "";
      position: absolute;
      bottom: -0.5rem;
      left: 10%;
      width: 80%;
      height: 1px;
      background-color: var(--color-shadow);
    }
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