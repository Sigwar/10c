<template>
  <p class="c-text">{{text}}</p>
</template>

<script>
export default {
  name: 'cText',
  props: [ 'text' ],
};
</script>

<style scoped
       lang="scss">
.c-text {
  line-height: 2;
  color: var(--font);
  width: 23.5rem;
}

@media screen and (max-width: 425px) {
  .c-text {
    font-size: 2.1rem;
    width: 100%;
  }
}
</style>