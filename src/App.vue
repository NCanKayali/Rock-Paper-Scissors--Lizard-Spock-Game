<template>
  <div class="game-arena">
    <h1 class="title">Rock Paper Scissors lizard Spock Game</h1>
    <div class="game-container">
      <div class="you">
        <h3 class="title who">You</h3>
        <p class="player-image">{{ selectedCard }}</p>
      </div>
      <div class="computer">
        <h3 class="title who">Computer</h3>
        <p class="computer-image" v-if="selectedCard !== null">
          {{ answer.image }}
        </p>
      </div>
    </div>
    <div class="result">
      <h3>Sonuç</h3>
      <p>{{ result }}</p>
    </div>

    <div>
      <transition-group name="rotateAll" appear class="items">
        <button
          @click="choice(item.image)"
          class="image"
          v-for="item in game"
          :key="item.image"
        >
          {{ item.image }}
        </button>
      </transition-group>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      game: [
        { image: "🧱" },
        { image: "📰" },
        { image: "✂️" },
        { image: "🦎" },
        { image: "🖖" },
      ],
      answer: {},
      selectedCard: null,
      result: null,
    };
  },
  methods: {
    random() {
      let answer = Math.ceil(Math.random() * this.game.length);
      this.answer = this.game[answer - 1];
    },
    choice(img) {
      this.random();
      this.selectedCard = img;
      if (this.selectedCard == this.answer.image) {
        this.result = "Kazandın";
      } else {
        this.result = "Kaybettin";
      }
      created();
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300&display=swap");
body {
  background-color: #ee4758;
  font-family: "Poppins", sans-serif;
}
.title {
  text-align: center;
}
.game-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 100px;
}
.you,
.computer {
  width: 350px;
  height: 250px;
  background-color: #292828;
  margin-right: 30px;
  border-radius: 30px;
}
.who {
  background-color: black;
  color: white;
  width: 350px;
  height: 50px;
  border-top-right-radius: 50px;
  border-top-left-radius: 50px;
  position: relative;
  bottom: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.result {
  text-align: center;
  margin-bottom: 80px;
  font-size: 30px;
  font-weight: 800;
}
.items {
  display: flex;
  justify-content: center;
  align-items: center;
}
.image {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100px;
  height: 75px;
  text-align: center;
  background-color: #292828;
  border-radius: 500px;
  margin-right: 20px;
  font-size: 30px;
  outline: none;
  border: none;
  cursor: pointer;
}
.computer-image,
.player-image {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 70px;
  margin: 0;
}

.rotateAll-enter-active {
  animation: rotate-x 2s ease-in-out forwards;
}
@keyframes rotate-x {
  from {
    transform: rotateX(0);
  }
  to {
    transform: rotateX(1080deg);
  }
}
</style>
