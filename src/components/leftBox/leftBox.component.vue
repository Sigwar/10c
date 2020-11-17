<template>
  <div class="c-left-box">
    <img alt="left-box-background"
         class="c-left-box__image"
         src="../../assets/img/picture.png">

    <div class="c-left-box__icon icon-lines"></div>
  </div>
</template>

<script>
export default {
  name: 'cLeftBox',
};
</script>

<style scoped
       lang="scss">

.c-left-box {
  position: relative;
  background: var(--background);
  height: 100%;
  width: 20rem;
  display: flex;
  align-items: center;

  &__image {
    object-fit: cover;
    position: absolute;
    opacity: 0.15;
    width: 20rem;
    height: 100%;
  }

  &__icon {
    z-index: 1;
    width: 20rem;
    height: 27.3rem;
    background-size: contain;
  }
}

@media screen and (max-width: 993px) {
  .c-left-box {
    display: none;
  }
}
</style>