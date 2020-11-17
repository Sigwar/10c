<template>
  <div :class="{'c-radio--active': isChecked}"
       class="c-radio">

    <span class="c-radio__label">{{label}}</span>

    <div :class="{'active': isChecked}"
         class="c-radio__box"></div>

    <input :name="name"
           :value="value"
           @click="changeValue"
           aria-label="Yes"
           class="c-radio__value"
           type="radio">
  </div>
</template>

<script>
export default {
  name: 'cRadio',
  props: [ 'label', 'name', 'isChecked', 'value' ],
  data() {
    return {
      someValue: false,
    };
  },
  methods: {
    changeValue(evt) {
      this.$emit('input', evt.target.value);
    },
  },
};
</script>

<style scoped lang="scss">
.c-radio {
  width: 50px;
  height: 50px;
  margin: 1rem 3rem 1rem 0;
  position: relative;
  box-sizing: border-box;

  &__label {
    position: absolute;
    top: 0;
    left: 0;
    transform: translate(50%, 100%);
    font-size: 14px;
  }

  &__box {
    top: 0;
    right: 0;
    z-index: 1;
    height: 20px;
    width: 20px;
    position: absolute;
    box-sizing: border-box;
    background: var(--white);
    border: 2px solid var(--gray);
    transform: translate(50%, 100%);
  }

  .active {
    border: 2px solid var(--secondary-color);

    &:after {
      content: '';
      width: 5px;
      height: 5px;
      border-radius: 50%;
      background: var(--secondary-color);
      position: absolute;
      left: 0;
      right: 0;
      transform: translate(100%, 100%);
    }
  }
}

input[type=radio] {
  left: 0;
  margin: 0;
  padding: 0;
  width: 50px;
  height: 50px;
  cursor: pointer;
  position: absolute;
  outline-offset: 0.1em;
  box-sizing: border-box;
  -webkit-appearance: none;
  outline: 2px solid var(--gray);
}

input[type=radio]:checked {
  display: inline-block;
  outline: 2px solid var(--secondary-color);
}

@media screen and (max-width: 425px) {
  .c-radio {
    width: 35px;
    height: 35px;

    &__box {
      height: 15px;
      width: 15px;
      transform: translate(70%, 80%);
    }

    &__label {
      transform: translate(25%, 50%);
    }

    .active {
      &:after {
        width: 5px;
        height: 5px;
        transform: translate(50%, 50%);
      }
    }
  }

  input[type=radio] {
    width: 35px;
    height: 35px;
  }
}
</style>