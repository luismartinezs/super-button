<template>
  <button class="transformable" @click="chargeKi">
    <span class="front" :class="transformation"></span>
  </button>
  <div>{{ki}}, {{transformation}}</div>
</template>

<script>
import { ref, computed } from "vue";

export default {
  name: "SuperButton",
  setup() {
    const ki = ref(0);
    const chargingKi = ref(false);

    const kiRequirements = {
      base: 0,
      ss1: 10,
      ss2: 25,
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
  display: block;
  width: 160px;
  height: 60px;
  transition: transform 300ms;
}

.transformable .base {
  background: hsl(200deg, 5%, 10%);
}

.transformable .ss1 {
  background: hsl(46, 100%, 52%);
}

.transformable .ss2 {
  background: hsl(54, 100%, 61%);
}

.transformable:active .front {
  transform: scale(1.1);
  transition: transform 50ms;
}
</style>
