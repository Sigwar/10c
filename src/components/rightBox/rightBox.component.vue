<template>
  <div class="c-right-box">

    <c-steps :active="active"
             :labels="labels"
             class="c-right-box__steps" />

    <transition name="slide-fade"
                transition-mode="out-in">

      <div v-if="active === 1">
        <c-text :text="loremIpsum" />
      </div>
    </transition>

    <transition name="slide-fade"
                transition-mode="out-in">

      <div class="c-right-box__step-2"
           v-if="active === 2">

        <c-text :text="textBox" />

        <form @submit="checkForm"
              action="#"
              id="cForm">

          <c-group-wrapper class="c-right-box__step-2__name"
                           label="Your name">

            <c-input :error="errors.name"
                     id="name"
                     v-model="name" />
          </c-group-wrapper>

          <c-group-wrapper class="c-right-box__step-2__mobile"
                           label="Mobile">

            <c-select :error="errors.prefix"
                      :options="mobileOptions"
                      v-model="prefix"></c-select>

            <c-input :error="errors.phoneNumber"
                     class="c-right-box__step-2__mobile__input"
                     id="mobile"
                     label=""
                     v-model="phoneNumber" />

          </c-group-wrapper>

          <c-group-wrapper class="c-right-box__step-2__chess"
                           label="Can you play chess?">

            <c-radio :is-checked="chess === 'Yes'"
                     @input="changeRadio"
                     label="Yes"
                     name="chess"
                     value='Yes' />

            <c-radio :is-checked="chess === 'No'"
                     @input="changeRadio"
                     label="No"
                     name="chess"
                     value='No' />

            <span class="c-right-box__step-2__chess__error"
                  v-if="errors.chess.length">{{errors.chess}}</span>
          </c-group-wrapper>


          <c-group-wrapper class="c-right-box__step-2__date"
                           label="Date of birth">

            <c-input class="c-right-box__step-2__date__day"
                     id="day"
                     v-model="day" />

            <c-select :options="monthOptions"
                      v-model="month"></c-select>

            <c-input :error="errors.date"
                     class="c-right-box__step-2__date__year"
                     id="year"
                     v-model="year" />

          </c-group-wrapper>
        </form>
      </div>
    </transition>

    <transition name="slide-fade"
                transition-mode="out-in">

      <div v-if="active === 3">
        <c-text :text="loremIpsum" />
      </div>
    </transition>

    <c-button button-text="Continue"
              class="c-right-box__button"
              form="cForm"
              native-type="submit" />
  </div>
</template>

<script>
import cButton       from '../button/button.component.vue';
import cSteps        from '../steps/steps.component.vue';
import cText         from '../text/text.component.vue';
import cInput        from '../input/input.component.vue';
import cRadio        from '../radio/radio.component.vue';
import cSelect       from '../select/select.component.vue';
import cGroupWrapper from '../groupWrapper/groupWrapper.component.vue';

export default {
  name: 'cRightBox',
  components: {
    cText,
    cRadio,
    cInput,
    cSteps,
    cButton,
    cSelect,
    cGroupWrapper,
  },
  data() {
    return {
      chess: null,
      name: '',
      phoneNumber: '',
      prefix: '',
      day: '',
      month: '',
      year: '',
      errors: {
        name: '',
        prefix: '',
        phoneNumber: '',
        chess: '',
        date: '',
      },
      mobileOptions: [ '+48 (PL)', '+34 (ES)', '+41 (CH)', '+31 (NL)' ],
      monthOptions: [ 'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December' ],
      active: 2,
      labels: [ { label: '', number: 1 }, { label: 'Personal', number: 2 }, { label: '', number: 3 } ],
      textBox: 'Provide personal information so that we can create a new account for you.',
      loremIpsum: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum',
    };
  },
  methods: {
    nextStep() {
      if (this.active === 2) {
        this.active += 1;
      } else if (this.active === 3) {
        this.active = 0;
      } else {
        this.active += 1;
      }
    },
    checkForm(e) {
      this.validateName();
      this.validatePrefix();
      this.validatePhoneNumber();
      this.validateChess();
      this.validateDate();

      let error = 0;
      Object.keys(this.errors).forEach(item => {
        if (this.errors[ item ] !== '') {
          error += 1;
        }
      });

      if (!error) {
        this.nextStep();
      }
      e.preventDefault();
    },
    validateName() {
      if (this.name.length <= 2) {
        this.errors.name = 'Minimum 3 characters';
      } else {
        this.errors.name = '';
      }
    },
    validatePrefix() {
      if (this.prefix.length) {
        this.errors.prefix = '';
      } else {
        this.errors.prefix = 'Should be selected';
      }
    },
    validateChess() {
      if (this.chess !== null) {
        this.errors.chess = '';
      } else {
        this.errors.chess = 'Should be selected';
      }
    },
    validatePhoneNumber() {
      this.phoneNumber = this.phoneNumber.replaceAll(' ', '');
      const number = parseInt(this.phoneNumber);
      if (isNaN(number)) {
        this.errors.phoneNumber = 'Incorrect number';
      } else if (this.phoneNumber.length !== 9) {
        this.errors.phoneNumber = 'Phone number must have 9 digits';
      } else {
        this.errors.phoneNumber = '';
      }
    },
    validateDate() {
      const myDay = parseInt(this.day);
      const myYear = parseInt(this.year);

      if (isNaN(myDay) || isNaN(myYear)) {
        this.errors.date = 'Incorrect date';
      } else if (this.day.length > 3 || this.year.length > 5) {
        this.errors.date = 'Incorrect date';
      } else if (!this.month.length) {
        this.errors.date = 'Incorrect date';
      } else {
        const now = new Date();
        const myDate = new Date(`${this.month} ${this.day}, ${this.year}`);
        if (!(myDate instanceof Date) || (myDate.toString() === 'Invalid Date')) {
          this.errors.date = 'Incorrect date';
        } else {
          let diff = now.getTime() - myDate.getTime();
          diff = Math.floor(diff / (1000 * 60 * 60 * 24 * 365.25));
          if (diff < 18) {
            this.errors.date = 'Less than 18 years old';
          } else {
            this.errors.date = '';
          }
        }
      }
    },
    changeRadio(newValue) {
      this.chess = newValue;
    },
  },
};
</script>

<style scoped
       lang="scss">

.slide-fade-enter-active {
  transition: var(--transition);
}

.slide-fade-enter {
  transform: translateX(4rem);
  opacity: 0;
}

.c-right-box {
  background: var(--white);
  box-sizing: border-box;
  padding: 3rem 3.6rem;
  width: 40.7rem;
  height: 100%;
  position: relative;

  &__step-2 {
    &__chess {
      display: flex;
      position: relative;

      &__error {
        position: absolute;
        bottom: -10px;
        left: 0;
        color: var(--error);
      }
    }

    &__date {
      &__day {
        margin-right: 1rem;
        width: 5rem;
      }

      &__year {
        width: 12rem;
      }
    }
  }

  &__button {
    position: absolute;
    bottom: 0;
    right: 0;
    transform: translate(20%, 50%);
  }
}

@media screen and (max-width: 992px) and (min-width: 641px) {
  .c-right-box {
    &__button {
      right: auto;
      transform: translate(50%, 50%);
    }
  }
}

@media screen and (max-width: 640px) and (min-width: 426px) {
  .c-right-box {
    &__button {
      right: auto;
      transform: translate(50%, 50%);
    }
  }
}

@media screen and (max-width: 425px) {
  .c-right-box {
    width: 45.5rem;

    &__step-2 {
      &__chess {
        &__error {
          font-size: 1.3rem;
        }
      }

      &__mobile {
        &__input {
          width: 20rem;
        }
      }
    }

    &__button {
      position: absolute;
      bottom: 0;
      left: auto;
      right: auto;
      transform: translate(0%, 50%);
    }

    &__steps {
      display: none;
    }
  }
}
</style>