<script setup>
  const props = defineProps({
    upgrades: Object
  })
</script>

<template>
  <div class="endScreen">
    <h1 class="endScreen__title" :style="{'animation-delay': '100ms'}">You Won!</h1>
    <img class="endScreen__icon" src="../assets/trophy.svg" :style="{'animation-delay': '600ms'}">
    <div class="endScreen__stats" :style="{'animation-delay': '1100ms'}">Power: {{ upgrades.power[0] }}</div>
    <div class="endScreen__stats" :style="{'animation-delay': '1600ms'}">Auto-clickers: {{ upgrades.autoClicker[0] }}</div>
    <div class="endScreen__stats" :style="{'animation-delay': '2100ms'}">Auto-clicker power: {{ upgrades.autoClickerPower[0] }}</div>
    <div class="endScreen__stats" :style="{'animation-delay': '2600ms'}">Auto-clicker speed: {{ upgrades.autoClickerSpeed[0] }}</div>
  </div>
</template>

<style scoped>
  .endScreen {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
    color: rgb(65, 184, 131);
    background: rgb(52, 73, 94);
  }

  .endScreen__title {
    font-size: 44px;
    opacity: 0;
  }

  .endScreen__icon {
    width: 200px;
    height: 200px;
    opacity: 0;
  }

  .endScreen__stats {
    font-size: 24px;
    opacity: 0;
  }

  .endScreen__title, .endScreen__icon, .endScreen__stats {
    animation: appearance 1s ease-in forwards;
  }

  @keyframes appearance {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
</style>
