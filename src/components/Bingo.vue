<template>
  <div class="notouch">
    <div class="bingo-cards-wrapper" v-if="answers.length > 0">
      <div class="bingo-grid-row" v-bind:key="y" v-for="y in tableHeight">
        <div class="bingo-card"
             @click="answerClick(answers[(y - 1)*tableHeight + (x-1)])"
             :class="isActive(answers[(y - 1)*tableHeight + (x-1)]) ? 'active' : ''"
             v-bind:key="x"
             v-for="x in tableWidth">
          <p class="mb-0">{{ answers[(y - 1)*tableHeight + (x-1)].answer }}</p>
        </div>
      </div>
    </div>
    <button type="button" class="btn btn-bingo mx-auto d-block mt-5" @click="newGame">
      Új kör
    </button>
    <ul class="rules">
      <b>Szabályok:</b>
      <li>A kör megnyeréséhez mind a 6 kártyádat ki kell pipálnod.</li>
      <li>Egy kártyát akkor pipálhatsz ki, ha az azon lévő szöveg elhangzott, vagy az adott tevékenység megtörtént.</li>
      <li>A saját kártyáidon lévő szövegeket nem mondhatod ki.</li>
      <li>Nem kérdezhetsz olyat, amire a válasz a kártyádon szerepel. De a beszélgetést terelheted úgy, hogy a válaszod felé menjen :)</li>
      <li>Bármikor kérhetsz magadnak új osztást, de olyankor a korábban elhangzottakat nem pipálhatod ki.</li>
      <li>Ha megvan mind a 6 kártyád, akkor bingód van. Ilyenkor ki kell mondanod hangosan, hogy "Bingó!"</li>
      <li>Ha valakinek bingója van, akkor mindenkinek új osztást kell kérnie.</li>
    </ul>
  </div>
</template>

<script>
import BingoElements from '../assets/items-custom'
import _ from 'lodash'

export default {
  mounted() {
    this.newGame()
  },
  data() {
    return {
      tableWidth: 6,
      tableHeight: 1,
      answers: [],
    }
  },
  methods: {
    isActive(element) {
      return element.count > 0
    },
    answerClick(element) {
      element.count++;

      if (this.isBingo) {
        alert('Bingó! Szólj, hogy új kör indul.')
      }
    },
    newGame() {
      const bingoAnswers = BingoElements.answers;
      this.answers = _.shuffle(bingoAnswers).slice(0, this.tableHeight * this.tableWidth).map((element) => {
        return {
          count: 0,
          answer: element
        }
      })
    },
  },
  computed: {
    isBingo() {
      const answers = this.answers.filter((a) => a.count === 0);
      return !answers.length;
    }
  }
}
</script>

<style>
.bingo-cards-wrapper {
  padding: 0 24px;
  margin: 0 auto;
}

.py-5 {
  margin-top: 0;
}

.bingo-grid-row {
  display: flex;
}

.bingo-card {
  margin: 24px 0;
  box-shadow: 0px 10px 15px -3px rgba(0, 0, 0, 0.1), 0px 4px 6px -4px rgba(0, 0, 0, 0.1);
  height: 72px;
  border-radius: 24px;
  border: none;
  cursor: pointer;
  text-align: center;
  background-color: #fff;
  font-weight: bold;
  font-size: 18px;
  word-wrap: break-word;
  background-repeat: no-repeat;
  background-position: 50%;
  background-size: cover;
  color: #1b1f27;
  flex: 1 1 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.bingo-card:hover {
  color: #1b1f27;
}

.bingo-card.active {
  background-color: hsla(0, 0%, 66.7%, 0.85);
  animation-name: bingo;
  animation-duration: 2s;
  animation-iteration-count: 1;
}

.btn-bingo {
  color: #eee;
  font-weight: bold;
  background-color: #27ae60;
  border: none;
  width: 50%;
  border-radius: 32px;
  font-size: 18px;
  padding: 16px;
}

.btn-bingo:focus {
  box-shadow: none;
  border: none;
}

.btn-bingo:hover {
  color: #eee;
  border: none;
}

.rules {
  margin: 48px 24px;
}

@keyframes bingo {
  0% {
    background-color: #fff;
  }

  100% {
    background-color: hsla(0, 0%, 66.7%, 0.85);
  }
}

@media screen and (max-width: 1800px) {
  .bingo-grid-row {
    display: block;
  }
}
</style>
