<script setup>
  import { ref, watch } from "vue";
  import Clicker from './components/Clicker.vue';
  import Store from './components/Store.vue';
  import EndScreen from './components/EndScreen.vue'

  let score = ref(0);
  let currentUpgrades = ref({
    power: [1, 1, 100],
    autoClicker: [0, 6, 16],
    autoClickerPower: [1, 15, 50],
    autoClickerSpeed: [1, 50, 10],
  });
  let isAutoWorking = ref(false);
  let intervalId = 0;
  let isEndScreen = ref(false);

  function handleClick(isAuto = false) {
    if (isAuto) {
      score.value += currentUpgrades.value.autoClicker[0] * currentUpgrades.value.autoClickerPower[0];
    } else {
      score.value += currentUpgrades.value.power[0];
    }
  }

  function handleUpgrade(stat) {
    if (stat === "power" && score.value >= currentUpgrades.value.power[1]) {
      score.value -= currentUpgrades.value.power[1];
      currentUpgrades.value.power = [
        currentUpgrades.value.power[0] + 1,
        (currentUpgrades.value.power[0] < 7
          ? currentUpgrades.value.power[1] * 2
          : Math.floor(currentUpgrades.value.power[1] * (currentUpgrades.value.power[0] / (currentUpgrades.value.power[0] - 1.5)))
        ),
        currentUpgrades.value.power[2]
      ];
    }

    if (stat === "auto" && score.value >= currentUpgrades.value.autoClicker[1]) {
      score.value -= currentUpgrades.value.autoClicker[1];
      currentUpgrades.value.autoClicker = [
        currentUpgrades.value.autoClicker[0] + 1,
        (currentUpgrades.value.autoClicker[0] < 4
          ? currentUpgrades.value.autoClicker[1] * 2
          : Math.floor(currentUpgrades.value.autoClicker[1] * (currentUpgrades.value.autoClicker[0] / (currentUpgrades.value.autoClicker[0] - 2.5)))
        ),
        currentUpgrades.value.autoClicker[2]
      ];
    }

    if (stat === "autoPower" && score.value >= currentUpgrades.value.autoClickerPower[1]) {
      score.value -= currentUpgrades.value.autoClickerPower[1];
      currentUpgrades.value.autoClickerPower = [
        currentUpgrades.value.autoClickerPower[0] + 1,
        (currentUpgrades.value.autoClickerPower[0] < 3
          ? currentUpgrades.value.autoClickerPower[1] * 2
          : Math.floor(currentUpgrades.value.autoClickerPower[1] * (currentUpgrades.value.autoClickerPower[0] / (currentUpgrades.value.autoClickerPower[0] - 1.7)))
        ),
        currentUpgrades.value.autoClickerPower[2]
      ];
    }

    if (stat === "autoSpeed" && score.value >= currentUpgrades.value.autoClickerSpeed[1]) {
      score.value -= currentUpgrades.value.autoClickerSpeed[1];
      currentUpgrades.value.autoClickerSpeed = [
        currentUpgrades.value.autoClickerSpeed[0] + 1,
        (currentUpgrades.value.autoClickerSpeed[0] < 3
          ? currentUpgrades.value.autoClickerSpeed[1] * 5
          : Math.floor(currentUpgrades.value.autoClickerSpeed[1] * (currentUpgrades.value.autoClickerSpeed[0] / (currentUpgrades.value.autoClickerSpeed[0] - 2)))
        ),
        currentUpgrades.value.autoClickerSpeed[2]
      ];
    }
  }

  function toggleAuto() {
    isAutoWorking.value = false;

    clearInterval(intervalId);

    setTimeout(() => {
      handleAuto();
      isAutoWorking.value = true;
    }, 0)
  }

  function handleAuto() {
    intervalId = setInterval(() => {handleClick(true)}, (1000 - (currentUpgrades.value.autoClickerSpeed[0] * 100 - 100)))
  }

  watch(() => currentUpgrades.value.autoClicker, () => {
    toggleAuto();
  })

  watch(() => currentUpgrades.value.autoClickerSpeed, () => {
    toggleAuto();
  })

  function handleWin() {
    if (score.value >= 500000) {
      isEndScreen.value = true
    }
  }
</script>

<template>
  <main class="app__game" v-if="!isEndScreen">
    <h1 class="app__score">
      Score: {{ score.toLocaleString(undefined) }}
    </h1>
    <Clicker :upgrades="currentUpgrades" :isAutoWorking="isAutoWorking" @player-clicked="handleClick" />
    <Store :upgrades="currentUpgrades" @upgrade="handleUpgrade" @win="handleWin" />
  </main>

  <EndScreen :upgrades="currentUpgrades" v-if="isEndScreen" />
</template>

<style scoped>
  .app__game {
    display: flex;
    flex-direction: column;
    height: 100%;
  }

  .app__score {
    position: absolute;
    color: rgb(65, 184, 131);
  }

  .app__button {
    width: 75px;
    height: 75px;
  }
</style>
