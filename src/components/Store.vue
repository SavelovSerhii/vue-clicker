<script setup>
  const props = defineProps({
    upgrades: Object
  })
</script>

<template>
  <div class="store">
    <h2 class="store__title">Store</h2>
    <section class="store__section">
      Basic
      <div class="store__container">
        <button class="store__button" @click="$emit('upgrade', 'power')" :disabled="props.upgrades.power[0] === props.upgrades.power[2]">
          Power: {{ props.upgrades.power[0] === props.upgrades.power[2] ? "MAX" : `${props.upgrades.power[0]} | ${props.upgrades.power[2]}` }}
          <br v-if="props.upgrades.power[0] !== props.upgrades.power[2]">
          <span v-if="props.upgrades.power[0] !== props.upgrades.power[2]">{{ props.upgrades.power[1] }}$</span>
        </button>
      </div>
    </section>

    <section class="store__section">
      Auto-Clickers
      <div class="store__container">
        <button class="store__button" @click="$emit('upgrade', 'auto')" :disabled="props.upgrades.autoClicker[0] === props.upgrades.autoClicker[2]">
          Auto-Clicker: {{ props.upgrades.autoClicker[0] === props.upgrades.autoClicker[2] ? "MAX" : `${props.upgrades.autoClicker[0]} | ${props.upgrades.autoClicker[2]}` }}
          <br v-if="props.upgrades.autoClicker[0] !== props.upgrades.autoClicker[2]">
          <span v-if="props.upgrades.autoClicker[0] !== props.upgrades.autoClicker[2]">{{ props.upgrades.autoClicker[1] }}$</span>
        </button>

        <button class="store__button" @click="$emit('upgrade', 'autoPower')" :disabled="props.upgrades.autoClickerPower[0] === props.upgrades.autoClickerPower[2]">
          Auto-Clicker Power: {{ props.upgrades.autoClickerPower[0] === props.upgrades.autoClickerPower[2] ? "MAX" : `${props.upgrades.autoClickerPower[0]} | ${props.upgrades.autoClickerPower[2]}` }}
          <br v-if="props.upgrades.autoClickerPower[0] !== props.upgrades.autoClickerPower[2]">
          <span v-if="props.upgrades.autoClickerPower[0] !== props.upgrades.autoClickerPower[2]">{{ props.upgrades.autoClickerPower[1] }}$</span>
        </button>

        <button class="store__button" @click="$emit('upgrade', 'autoSpeed')" :disabled="props.upgrades.autoClickerSpeed[0] === props.upgrades.autoClickerSpeed[2]">
          Auto-Clicker Speed: {{ props.upgrades.autoClickerSpeed[0] === props.upgrades.autoClickerSpeed[2] ? "MAX" : `${props.upgrades.autoClickerSpeed[0]} | ${props.upgrades.autoClickerSpeed[2]}` }}
          <br v-if="props.upgrades.autoClickerSpeed[0] !== props.upgrades.autoClickerSpeed[2]">
          <span v-if="props.upgrades.autoClickerSpeed[0] !== props.upgrades.autoClickerSpeed[2]">{{ props.upgrades.autoClickerSpeed[1] }}$</span>
        </button>
      </div>
    </section>

    <section class="store__section">
      Trophy
      <div class="store__container">
        <button class="store__button store__button--gold" @click="$emit('win')">
          500 000$
        </button>
      </div>
    </section>

    <!-- <section class="store__section" v-if="props.upgrades.autoClicker[0]">
      Toggle Auto-Clickers
      <button class="store__button store__button--red" @click="$emit('toggleAuto')" v-if="!props.isAutoWorking">
        Off
      </button>

      <button class="store__button store__button--green" @click="$emit('toggleAuto')" v-if="props.isAutoWorking">
        On
      </button>
    </section> -->
  </div>
</template>

<style scoped>
  .store {
    position: relative;
    display: flex;
    gap: 100px;
    padding: 40px 20px;
    height: 25vh;
    color: rgb(52, 73, 94);
    background: rgb(65, 184, 131);
    border-top: 5px solid rgb(0, 0, 0);
  }

  .store__title {
    position: absolute;
    top: 5px;
  }

  .store__section {
    display: flex;
    flex-direction: column;
    gap: 5px;
  }

  .store__container {
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    gap: 5px;
    max-height: 150px;
  }

  .store__button {
    width: 225px;
    height: 50px;
    color: rgb(65, 184, 131);
    background: rgb(89, 125, 161);
    border: 2px solid rgb(52, 73, 94);
    border-radius: 20px;
    font-size: 16px;
    cursor: pointer;
    user-select: none;
  }

  .store__button--gold {
    background: rgb(255, 215, 0);
    font-size: 24px;
    font-weight: bold;
  }

  .store__button--red {
    color: rgb(255, 255, 255);
    background: rgb(255, 0, 0);
    font-size: 20px;
  }

  .store__button--green {
    color: rgb(255, 255, 255);
    background: rgb(0, 128, 0);
    font-size: 20px;
  }
</style>