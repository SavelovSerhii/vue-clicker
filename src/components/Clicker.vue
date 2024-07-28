<script setup>
  import { ref, watch } from 'vue';

  const props = defineProps({
    upgrades: Object,
    isAutoWorking: Boolean
  })

  const animationSpeed = ref(`${1 - (props.upgrades.autoClickerSpeed[0] / 10 - 0.1)}s`);

  watch(() => props.upgrades.autoClickerSpeed, () => {
    animationSpeed.value = `${1 - (props.upgrades.autoClickerSpeed[0] / 10 - 0.1)}s`;
  })
</script>

<template>
  <div class="clicker">
    <button class="clicker__button" @click="$emit('playerClicked')">
      <img class="clicker__icon" alt="icon" src="../assets/logo.svg" />

      <div class="autoclicker">
        <div class="autoclicker__container autoclicker__container--top">
          <template v-for="auto in (upgrades.autoClicker[0] <= 4 ? upgrades.autoClicker[0] : 4)" v-bind:key="auto">
            <img
              class="autoclicker__icon autoclicker__icon--top"
              :class="{'autoclicker__icon--workTop': isAutoWorking}"
              :style="{'animation-duration': animationSpeed}"
              alt="icon"
              src="../assets/logo.svg"
            />
          </template>
        </div>

        <div class="autoclicker__container autoclicker__container--right">
          <template v-for="auto in (upgrades.autoClicker[0] <= 4 ? 0 : upgrades.autoClicker[0] > 8 ? 4 : upgrades.autoClicker[0] - 4)" v-bind:key="auto">
            <img
              class="autoclicker__icon autoclicker__icon--right"
              :class="{'autoclicker__icon--workRight': isAutoWorking}"
              alt="icon"
              src="../assets/logo.svg"
            />
          </template>
        </div>

        <div class="autoclicker__container autoclicker__container--bottom">
          <template v-for="auto in (upgrades.autoClicker[0] <= 8 ? 0 : upgrades.autoClicker[0] > 12 ? 4 : upgrades.autoClicker[0] - 8)" v-bind:key="auto">
            <img
              class="autoclicker__icon autoclicker__icon--bottom"
              :class="{'autoclicker__icon--workBottom': isAutoWorking}"
              alt="icon"
              src="../assets/logo.svg"
            />
          </template>
          
        </div>

        <div class="autoclicker__container autoclicker__container--left">
          <template v-for="auto in (upgrades.autoClicker[0] <= 12 ? 0 : upgrades.autoClicker[0] - 12)" v-bind:key="auto">
            <img
              class="autoclicker__icon autoclicker__icon--left"
              :class="{'autoclicker__icon--workLeft': isAutoWorking}"
              alt="icon"
              src="../assets/logo.svg"
            />
          </template>
        </div>
      </div>
    </button>
  </div>
</template>

<style scoped>
  .clicker {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 75vh;
    background: rgb(52, 73, 94);
  }

  .clicker__button {
    position: relative;
    z-index: 1;
    height: 200px;
    width: 220px;
    background: rgb(89, 125, 161);
    border-radius: 25px;
    cursor: pointer;
  }

  .clicker__icon {
    height: 150px;
    width: 150px;
    user-select: none;
    pointer-events: none;
  }

  .autoclicker {
    position: absolute;
    top: -50px;
    right: -50px;
    bottom: -50px;
    left: -50px;
    z-index: 0;
    display: grid;
    grid-template:
      "top top top" 66px
      "left . right" 164px
      "bottom bottom bottom" 66px / 92px 132px 92px;
    user-select: none;
    pointer-events: none;
  }

  .autoclicker__container {
    position: relative;
    display: flex;
    justify-content: center;
  }

  .autoclicker__container--top {
    grid-area: top;
    height: 64px;
  }

  .autoclicker__container--right {
    grid-area: right;
    flex-direction: column;
    align-items: flex-end;
  }

  .autoclicker__container--bottom {
    grid-area: bottom;
    align-items: flex-end;
    height: 64px;
  }

  .autoclicker__container--left {
    grid-area: left;
    flex-direction: column-reverse;
  }

  .autoclicker__icon {
    position: relative;
    height: 40px;
    width: 40px;
  }

  .autoclicker__icon--right {
    rotate: 90deg;
  }

  .autoclicker__icon--bottom {
    rotate: 180deg;
  }

  .autoclicker__icon--left {
    rotate: 270deg;
  }

  .autoclicker__icon--workTop {
    animation: workTop 1s cubic-bezier(1.000, 0.005, 1.000, 1.000) infinite;
  }

  .autoclicker__icon--workRight {
    animation: workRight 1s cubic-bezier(1.000, 0.005, 1.000, 1.000) infinite;
    animation-duration: v-bind(animationSpeed);
  }

  .autoclicker__icon--workBottom {
    animation: workBottom 1s cubic-bezier(1.000, 0.005, 1.000, 1.000) infinite;
    animation-duration: v-bind(animationSpeed);
  }

  .autoclicker__icon--workLeft {
    animation: workLeft 1s cubic-bezier(1.000, 0.005, 1.000, 1.000) infinite;
    animation-duration: v-bind(animationSpeed);
  }

  @keyframes workTop {
    from {top: 10px;}
    to {top: -15px;}
  }

  @keyframes workRight {
    from {right: 10px;}
    to {right: -15px;}
  }

  @keyframes workBottom {
    from {bottom: 10px;}
    to {bottom: -15px;}
  }

  @keyframes workLeft {
    from {left: 10px;}
    to {left: -15px;}
  }
</style>
