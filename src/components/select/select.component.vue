<template>
  <div class="c-select">
    <label>
      {{label}}
      <select :value="value"
              @change="changeValue">

        <option :key="index"
                v-for="(option, index) in options">{{option}}
        </option>
      </select>
      <span class="c-select__error"
            v-if="error !== ''">{{error}}</span>
    </label>
  </div>
</template>

<script>
export default {
  name: 'cSelect',
  props: [ 'options', 'label', 'error' ],
  data() {
    return {
      value: '',
    };
  },
  methods: {
    changeValue(evt) {
      this.$emit('input', evt.target.value);
    },
  },
};
</script>

<style scoped
       lang="scss">
.c-select {
  position: relative;

  &__error {
    position: absolute;
    left: 0;
    bottom: -17px;
    color: var(--error);
  }
}

select {
  padding: .5rem;
  height: 100%;
  width: 7.8rem;
  border: none;
  border-bottom: 2px solid var(--gray);
  cursor: pointer;
  margin-right: 2rem;
}

select:focus {
  outline: none;
}

@media screen and (max-width: 425px) {
  .c-select {
    margin: 0 1rem 0 0;

    &__error {
      position: absolute;
      bottom: -12px;
      color: var(--error);
      font-size: 1.3rem;
    }
  }

  select {
    width: 100%;
    margin-right: 4rem;
  }
}
</style>