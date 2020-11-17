<template>
  <div class="app"
       id="app">

    <div class="app__container">
      <c-title title="Your account" />

      <c-wrapper>
        <c-left-box />
        <c-right-box />
      </c-wrapper>
    </div>
  </div>
</template>

<script>
import cWrapper  from './components/wrapper/wrapper.component.vue';
import cLeftBox  from './components/leftBox/leftBox.component.vue';
import cRightBox from './components/rightBox/rightBox.component.vue';
import cTitle    from './components/title/title.component.vue';

export default {
  name: 'App',
  components: {
    cTitle,
    cLeftBox,
    cWrapper,
    cRightBox,
  },
};
</script>

<style lang="scss">
@import 'assets/style/main';

.app {
  height: 100vh;
  width: 100vw;
  display: flex;
  align-items: center;
  justify-content: center;

  &__container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
}
</style>
