<template>
  <div class="c-group-wrapper">
    <span class="c-group-wrapper__label">{{label}}</span>

    <div class="c-group-wrapper__container">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'cGroupWrapper',
  props: [ 'label' ],
};
</script>

<style scoped lang="scss">
.c-group-wrapper {
  margin-top: 2rem;
  display: flex;
  flex-direction: column;

  &__label {
    font-size: .8rem;
    color: var(--label-color);
  }

  &__container {
    display: flex;
  }
}

@media screen and (max-width: 425px) {
  .c-group-wrapper {
    margin-top: 3.5rem;

    &__label {
      font-size: 1.7em;
    }
  }
}
</style>