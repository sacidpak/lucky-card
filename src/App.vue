<template>
  <div>
    <transition-group name="slideContainer" mode="out-in">
      <component
        @activeComponentEvent="activeComponent = $event"
        :is="activeComponent"
        key="mainComponent"
      ></component>
      <canvas id="canvas" key="canvas" v-show="activeComponent == 'app-celebrate'"></canvas>
    </transition-group>
  </div>
</template>

<script>
import GameCards from "./components/GameCards.vue";
import Celebrate from "./components/Celebrate.vue";
import Fail from "./components/Fail.vue";

export default {
  name: "app",
  components: {
    appGameCard: GameCards,
    appCelebrate: Celebrate,
    appFail: Fail
  },
  data() {
    return {
      activeComponent: "appGameCard"
    };
  }
};
</script>

<style>
body {
  font-family: sans-serif;
}

.slideContainer-enter {
}

.slideContainer-enter-active {
  animation: slide-in 0.3s ease-out forwards;
}

.slideContainer-leave {
}

.slideContainer-leave-active {
  animation: slide-out 0.3s ease-out forwards;
}

@keyframes slide-in {
  from {
    transform: translateX(-1000px);
    opacity: 0;
  }
  to {
    transform: translateX(0px);
    opacity: 1;
  }
}

@keyframes slide-out {
  from {
    transform: translateX(0px);
    opacity: 1;
  }
  to {
    transform: translateX(1000px);
    opacity: 0;
  }
}
</style>
