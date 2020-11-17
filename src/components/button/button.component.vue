<template>
  <button @click="handleClick"
          class="c-button">

      <span class="c-button__text">
          {{buttonText}}
      </span>

    <span class="c-button__icon">
          <span class="icon icon-arrow"></span>
      </span>
  </button>
</template>

<script>
export default {
  name: 'cButton',
  props: [ 'buttonText' ],
  methods: {
    handleClick(evt) {
      this.$emit('click', evt);
    },
  },
};
</script>

<style scoped
       lang="scss">
.c-button {
  margin: 0;
  padding: 0;
  border: none;
  display: flex;
  height: 3.7rem;
  cursor: pointer;
  background: none;
  align-items: center;
  background: var(--primary-color);

  &__text {
    height: 100%;
    display: flex;
    width: 13.5rem;
    padding: 1.1rem;
    color: var(--white);
    align-items: center;
    box-sizing: border-box;
    justify-content: center;
    text-transform: uppercase;
  }

  .icon {
    width: 100%;
    height: 100%;
    display: block;
  }

  &__icon {
    width: 3.7rem;
    height: 3.7rem;
    background: var(--primary-color-light);
  }

  &:hover {
    .c-button__icon {
      background: var(--primary-color);
    }
  }

  &:focus,
  &:active {
    outline: none;
  }
}

@media screen and (max-width: 425px) {
  .c-button {
    height: 6.5rem;
    width: 37rem;

    &__text {
      width: 100%;
    }

    &__icon {
      height: 100%;
      width: 7.6rem;
    }
  }
}
</style>