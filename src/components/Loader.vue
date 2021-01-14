<template>
  <div class="loader" :class="visible">
    <span></span>
    <span></span>
    <span></span>
    <span></span>
  </div>
</template>

<script>
export default {
  name: 'Loader',

  props: {
    visible: String
  }
};
</script>

<style lang="scss" scoped>
.loader {
  display: none;
  text-align: center;
  border-radius: 100%;
  margin: 2em 0;

  &.visible {
    display: block;
  }

  span {
    display: inline-block;
    width: 5px;
    height: 20px;
    margin: 0 0.2em;
    background-color: #f38f1d;

    animation: grow 0.6s ease-in-out infinite;

    &:nth-child(2) {
      animation-delay: 0.1s;
    }
    &:nth-child(3) {
      animation-delay: 0.2s;
    }
    &:nth-child(4) {
      animation-delay: 0.3s;
    }
  }
}

/* ANIMATIONS */
@keyframes grow {
  0%,
  100% {
    -webkit-transform: scaleY(1);
    -ms-transform: scaleY(1);
    -o-transform: scaleY(1);
    transform: scaleY(1);
  }

  50% {
    -webkit-transform: scaleY(1.8);
    -ms-transform: scaleY(1.8);
    -o-transform: scaleY(1.8);
    transform: scaleY(1.8);
  }
}
</style>
