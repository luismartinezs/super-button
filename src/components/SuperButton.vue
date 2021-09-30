<template>
  <button class="transformable" @click="chargeKi">
    <span class="front ss1" :class="transformation">Push me</span>
  </button>
  <div>{{ki}}, {{transformation}}</div>
</template>

<script>
import { ref, computed } from "vue";

const easyMode = true;

export default {
  name: "SuperButton",
  setup() {
    const ki = ref(0);
    const chargingKi = ref(false);

    const kiRequirements = {
      base: 0,
      ss1: easyMode ? 1 : 10,
      ss2: easyMode ? 5 : 25,
    };

    const transformation = computed(() => {
      return Object.entries(kiRequirements).reduce((acc, [form, kiReq]) => {
        if (kiReq < ki.value && kiRequirements[acc] < kiRequirements[form]) {
          acc = form;
        }
        return acc;
      }, "base");
    });

    const triggerKiCharging = () => {
      if (!chargingKi.value) {
        let timer = setInterval(() => {
          ki.value = ki.value - 1;
          if (ki.value === 0) {
            clearInterval(timer);
            chargingKi.value = false;
          }
        }, 1000);
      }
      chargingKi.value = true;
    };

    const chargeKi = () => {
      triggerKiCharging();
      ki.value = ki.value + 1;
    };

    return {
      transformation,
      chargeKi,
      ki,
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.transformable {
  border: none;
  background: transparent;
  cursor: pointer;
  padding: 0;
  outline-offset: 5px;
  will-change: transform;
}

.transformable:focus:not(:focus-visible) {
  outline: none;
}

.transformable .front {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 1.5rem;
  width: 160px;
  height: 60px;
  transition: transform 300ms;
}

.transformable .base {
  background: hsl(200deg, 5%, 10%);
  color: white;
}

.transformable .ss1 {
  --color: hsl(46, 100%, 52%);
  background: var(--color);
  color: hsl(20, 100%, 33%);
  box-shadow: 0 0 10px var(--color), 0 0 20px var(--color),
    0 0 40px var(--color), 0 0 80px var(--color), 0 0 160px var(--color);
}

.transformable .ss2 {
  --color: hsl(54, 100%, 61%);
  background: var(--color);
  color: hsl(30, 62%, 39%);
  box-shadow: 0 0 10px var(--color), 0 0 20px var(--color),
    0 0 40px var(--color), 0 0 80px var(--color), 0 0 160px var(--color);
}

.transformable:active .front {
  transform: scale(1.1);
  transition: transform 50ms;
}
</style>
