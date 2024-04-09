<template>
  <v-container >
    <div class="text-center">
      <h1 class="text-h2 font-weight-bold">Chifoumi</h1>
      <h4>Jouez un coup ! ;)</h4>
      <h1>{{ resultSentence }}</h1>
      <h3>{{ userScore }} - {{ botScore }}</h3>
    </div>
    <div class="py-4" />

    <v-row style="justify-content: center; align-items: center; gap: 20px;">
      <v-btn class="m-8 p-4" variant="outlined" color="grey" @click="play(1)">
        <h1>Pierre</h1>
      </v-btn>
      <v-btn class="m-8 p-4" variant="outlined" color="green" @click="play(2)">
        <h1>Feuille</h1>
      </v-btn>
      <v-btn class="m-8 p-4" variant="outlined" color="red" @click="play(3)">
        <h1>Ciseau</h1>
      </v-btn>
    </v-row>

    <div class="text-center mt-8" style="align-items: center;">
      <v-row>
        <v-card width="200" class="mx-auto p-8 ma-4" elevation="10">
          <h2> User : {{ userChoice === 1 ? 'Pierre' : userChoice === 2 ? 'Feuille' : userChoice === 3 ? 'Ciseau' : "" }}</h2>
        </v-card>
        <v-card width="200" class="mx-auto p-8 ma-4" elevation="10" >
          <h2>Bot : {{ botChoice === 1 ? 'Pierre' : botChoice === 2 ? 'Feuille' : botChoice === 3 ? 'Ciseau' : ""}}</h2>
        </v-card>
      </v-row>
      <div class="text-center mt-8" style="align-items: center;">
      <v-row>
        <v-card>
          <v-card-title>
            <h1>Historique</h1>
          </v-card-title>
          <v-card-text>
            <hr>
            <h3 v-for="score in scores" :key="score">{{ score.user === 1 ? 'Pierre' : score.user === 2 ? 'Feuille' : score.user === 3 ? 'Ciseau' : "" }} vs {{ score.bot === 1 ? 'Pierre' : score.bot === 2 ? 'Feuille' : score.bot === 3 ? 'Ciseau' : "" }} : Vous avez {{ score.result }}</h3>
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
      console.log(this.userScore, this.botScore);
      this.scores.push({user: this.userChoice, bot: this.botChoice, result: this.resultSentence})
    
    },
    setbotChoice() {
      return Math.floor(Math.random() * (3 - 1 + 1)) + 1
    }
  }
}
</script>
