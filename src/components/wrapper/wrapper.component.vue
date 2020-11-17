<template>
  <div class="c-wrapper">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'cWrapper',
};
</script>

<style scoped
       lang="scss">

.c-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 40.4rem;
}

@media screen and (max-width: 425px) {
  .c-wrapper {
    height: 65rem;
  }
}
</style>