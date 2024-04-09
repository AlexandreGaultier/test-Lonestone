<template>
  <v-container>
    <div class="text-center">
      <h1 class="text-h2 font-weight-bold">Chifoumi</h1>
      <h3><i>Choisissez un bouton</i></h3>
      <h1>{{ resultSentence }}</h1>
      <h3>{{ userScore }} - {{ botScore }}</h3>
    </div>
    <div class="py-4" />

    <v-row style="justify-content: center; align-items: center; gap: 20px;">
      <v-btn size="x-large" icon="mdi-hexagon" class="m-8 p-4" variant="outlined" color="grey" @click="play(1)">
      </v-btn>
      <v-btn size="x-large" icon="mdi-leaf" class="m-8 p-4" variant="outlined" color="green" @click="play(2)">
        <v-icon icon="mdi-leaf"></v-icon>
      </v-btn>
      <v-btn size="x-large" icon="mdi-content-cut" class="m-8 p-4" variant="outlined" color="primary" @click="play(3)">
      </v-btn>
    </v-row>

    <div class="text-center mt-8" style="align-items: center;">
      <v-row>
        <v-card width="200" class="mx-auto p-8 ma-4" elevation="10">
          <h2> Votre choix : {{ userChoice === 1 ? 'Pierre' : userChoice === 2 ? 'Feuille' : userChoice === 3 ? 'Ciseau' : "" }}</h2>
        </v-card>
        <v-card width="200" class="mx-auto p-8 ma-4" elevation="10">
          <h2>Choix du Bot : {{ botChoice === 1 ? 'Pierre' : botChoice === 2 ? 'Feuille' : botChoice === 3 ? 'Ciseau' : "" }}</h2>
        </v-card>
      </v-row>
      <div class="text-center mt-8" style="align-items: center;">
        <v-row>
          <v-card>
            <v-card-title>
              <h1>Historique des scores</h1>
            </v-card-title>
            <v-card-text>
              <hr>
              <div v-for="score in scores" :key="score" class="ma-4 align-start">
                <h3 class="py-2">Vous : {{ score.user === 1 ? 'Pierre' : score.user === 2 ? 'Feuille' : score.user === 3 ? 'Ciseau' : "" }} - Bot : {{ score.bot === 1 ? 'Pierre' : score.bot === 2 ? 'Feuille' : score.bot === 3 ? 'Ciseau' : "" }}</h3>
                <h4>Vous avez {{ score.result }}.</h4>
                <h5>{{ score.userScore }} - {{ score.botScore }}</h5>
              </div>
            </v-card-text>
          </v-card>
        </v-row>
      </div>
    </div>
  </v-container>
</template>

<script>
export default {
  name: 'Chifoumi',
  data() {
    return {
      userChoice: "",
      botChoice: "",
      resultSentence: "",
      scores: [],
      userScore: 0,
      botScore: 0
    }
  },
  methods: {
    play(choice) {
      this.userChoice = choice
      this.botChoice = this.setbotChoice()

      if (this.userChoice === 1) {
        if (this.botChoice === 1) {
          this.resultSentence = "Egalité"
          this.resetValues()
        } else if (this.botChoice === 2) {
          this.resultSentence = "Perdu"
          this.botScore += 1
          this.resetValues()
        } else if (this.botChoice === 3) {
          this.resultSentence = "Gagné"
          this.userScore += 1
          this.resetValues()
        }
      } else if (this.userChoice === 2) {
        if (this.botChoice === 1) {
          this.resultSentence = "Gagné"
          this.userScore += 1
          this.resetValues()

        } else if (this.botChoice === 2) {
          this.resultSentence = "Egalité"
          this.resetValues()

        } else if (this.botChoice === 3) {
          this.resultSentence = "Perdu"
          this.botScore += 1
          this.resetValues()

        }
      } else if (this.userChoice === 3) {
        if (this.botChoice === 1) {
          this.resultSentence = "Perdu"
          this.botScore += 1
          this.resetValues()

        } else if (this.botChoice === 2) {
          this.resultSentence = "Gagné"
          this.userScore += 1
          this.resetValues()

        } else if (this.botChoice === 3) {
          this.resultSentence = "Egalité"
          this.resetValues()

        }
      }
    },
    resetValues() {
      this.scores.push({ user: this.userChoice, bot: this.botChoice, result: this.resultSentence, userScore: this.userScore, botScore: this.botScore })
    },
    setbotChoice() {
      return Math.floor(Math.random() * (3 - 1 + 1)) + 1
    }
  }
}
</script>
