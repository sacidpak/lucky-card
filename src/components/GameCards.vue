<template>
  <div class="game-area">
    <!-- <p>{{answer}}</p>   -->
    <h1 class="title">Closed card <span>which</span> one <strong>?</strong></h1>
    <h4 class="description">Select one opened card and click closed card</h4>
    <div class="container">
      <transition-group name="rotate-all" class="card-container" appear>
        <app-card
          :class="{'shadow' : selectedCard == card.id}"
          v-for="card in cards"
          :key="card.id"
          :card="card"
          @click.native="selectedCard = card.id"
        ></app-card>
      </transition-group>
    </div>
    <div class="container">
      <transition name="rotate" mode="out-in">
        <component @click.native="showCard(answer)" :is="activeCard" :card="answer"></component>
      </transition>
    </div>
  </div>
</template>
<script>
import Card from "./Card.vue";
import DefaultCard from "./DefaultCard.vue";
export default {
  components: {
    appCard: Card,
    appDefaultCard: DefaultCard
  },
  data() {
    return {
      cards: [
        { id: 1, component: "app-card", img: "/src/assets/card-1.jpg" },
        { id: 2, component: "app-card", img: "/src/assets/card-2.jpg" },
        { id: 3, component: "app-card", img: "/src/assets/card-3.jpg" },
        { id: 4, component: "app-card", img: "/src/assets/card-4.jpg" },
        { id: 5, component: "app-card", img: "/src/assets/card-5.jpg" }
      ],
      selectedCard: null,
      answer: {},
      activeCard: "appDefaultCard"
    };
  },
  methods: {
    showCard(answer) {
      if (this.selectedCard == null) {
        alert("Please select card!");
      } else {
        this.activeCard = answer.component;
        setTimeout(() => {
          if (answer.id == this.selectedCard) {
              this.$emit("activeComponentEvent","app-celebrate");
          }else {
              this.$emit("activeComponentEvent","app-fail");
          }
        }, 1000);
      }
    }
  },
  created() {
    let answer = Math.ceil(Math.random() * this.cards.length);
    this.answer = this.cards[answer - 1];
  }
};
</script>

<style scoped>
.title {
  text-align: center;
  color: rosybrown;
}

.title span {
  color: mediumpurple;
}

.title strong {
  color: darkred;
}

.description {
  text-align: center;
  color: gray;
}

.container,
.card-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 50px;
}

.shadow {
  box-shadow: 0px 5px 48px #38969f !important;
  transition: box-shadow 0.5s;
}

.rotate-all-enter {
}

.rotate-all-enter-active {
  animation: rotate-all ease-in-out 2s forwards;
}

.rotate-all-leave {
}

.rotate-all-leave-active {
}

.rotate-enter {
}

.rotate-enter-active {
  animation: rotate-in ease-in-out 0.5s forwards;
}

.rotate-leave {
}

.rotate-leave-active {
  animation: rotate-out ease-in-out 0.5s forwards;
}

@keyframes rotate-all {
  from {
    transform: rotateY(0);
  }
  to {
    transform: rotateY(1080deg);
  }
}

@keyframes rotate-in {
  from {
    transform: rotateY(90deg);
  }
  to {
    transform: rotateY(0deg);
  }
}

@keyframes rotate-out {
  from {
    transform: rotateY(0);
  }
  to {
    transform: rotateY(90deg);
  }
}
</style>

