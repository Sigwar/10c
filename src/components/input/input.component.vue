<template>
  <div class="c-input">

    <input :id="id"
           :value="value"
           @blur="changeInputStyle"
           @focus="changeInputStyle"
           @input="handleInput"
           class="c-input__value">

    <div :class="{'show-border': isActive, 'error-border': error}"
         class="c-input__border"></div>

    <span class="c-input__error"
          v-if="error !== ''">
    {{error}}
    </span>
  </div>
</template>

<script>
export default {
  name: 'cInput',
  props: [ 'error', 'value', 'id' ],
  data() {
    return {
      content: this.value,
      isActive: false,
    };
  },
  methods: {
    handleInput(evt) {
      this.$emit('input', evt.target.value);
    },
    changeInputStyle() {
      this.isActive = !this.isActive;
    },
  },
};
</script>

<style scoped
       lang="scss">
.c-input {
  display: flex;
  flex-direction: column;
  position: relative;
  width: 100%;

  &__value {
    z-index: 1;
    border: none;
    font-size: 1.6rem;
    font-weight: var(--light);
    padding: .5rem 1rem .5rem;
    background: var(--transparent);
    border-bottom: 2px solid var(--gray);

    &:focus {
      outline: none;
    }
  }

  &__border {
    left: 0;
    bottom: 0;
    z-index: 2;
    height: 2px;
    width: 100%;
    position: absolute;
    transform: scaleX(0);
    transform-origin: 0 0;
    transition: all .25s ease;
    background: var(--primary-color);
  }

  &__error {
    position: absolute;
    bottom: -17px;
    color: var(--error);
  }

  .show-border {
    transform: scaleX(1);
  }
}

@media screen and (max-width: 425px) {
  .c-input {
    &__value {
      z-index: 1;
      border: none;
      font-size: 2.6rem;
      border-bottom: 2px solid var(--gray);
    }

    &__error {
      position: absolute;
      bottom: -12px;
      color: var(--error);
      font-size: 1.3rem;
    }
  }
}
</style>