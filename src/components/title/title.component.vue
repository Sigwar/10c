<template>
  <h1 class="c-title-header">{{title}}</h1>
</template>

<script>
export default {
  name: 'Title',
  props: [ 'title' ],
};
</script>

<style scoped
       lang="scss">

.c-title-header {
  color: var(--white);
  font-weight: var(--light);
  font-size: 3.5rem;
}

</style>