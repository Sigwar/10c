<template>
  <div class="c-steps">

    <div :key="index"
         class="c-steps__item"
         v-for="(item, index) in labels">

      <div :class="{'c-steps__item__line--active': index + 1 === active}"
           class="c-steps__item__line"></div>

      <span class="c-steps__item__number">{{index+1}}</span>
      <span class="c-steps__item__label">{{item.label}}</span>
    </div>

  </div>
</template>

<script>
export default {
  name: 'cSteps',
  props: [ 'labels', 'active' ],
};
</script>

<style scoped
       lang="scss">
.c-steps {
  position: absolute;
  right: -4.5rem;

  &__item {
    margin-bottom: 4.8rem;
    color: var(--white);

    &__line,
    &__number,
    &__label {
      display: block;
      font-weight: var(--light);
    }

    &__number,
    &__label {
      margin-left: .6rem;
      padding: .1rem 0;
    }

    &__line {
      width: 2.6rem;
      height: 2px;
      background: var(--gray);
      opacity: 0.2;

      &--active {
        background: var(--secondary-color);
        opacity: 1;
      }
    }
  }
}
</style>