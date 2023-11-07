<script setup lang="ts"></script>

<template>
  <div class="bg">
    <div :class="`layer-${item}`" v-for="item in 5" :key="item" />
  </div>
</template>

<style scoped lang="scss">
$count: 1000;
$time: 1000;

.bg {
  width: 100%;
  height: 100%;
  background: #000;
}

@function getBoxShadow($n) {
  $box-shadow: #{random(100)}vw #{random(100)}vh #fff;

  @for $i from 2 through $n {
    $box-shadow:
      #{$box-shadow},
      #{random(100)}vw #{random(100)}vh #fff;
  }
  @return $box-shadow;
}

@for $i from 1 through 5 {
  $size: $i + px;
  $count: floor(calc($count / 2));
  $time: floor(calc($time / 2));

  .layer-#{$i} {
    width: $size;
    height: $size;
    background-color: #fff;
    border-radius: 50%;
    box-shadow: getBoxShadow($count);
    animation:
      moveTop #{$time}s linear infinite,
      opacity #{calc($time * 2)}s linear infinite;
    &::before {
      position: fixed;
      top: 100vh;
      width: inherit;
      height: inherit;
      background-color: inherit;
      border-radius: inherit;
      box-shadow: inherit;
    }
  }
}

@keyframes moveTop {
  100% {
    transform: translateY(-100vh);
  }
}

@keyframes opacity {
  0%,
  20%,
  40%,
  60%,
  80%,
  100% {
    opacity: 1;
  }

  10%,
  30%,
  50%,
  70%,
  90% {
    opacity: 0;
  }
}
</style>
