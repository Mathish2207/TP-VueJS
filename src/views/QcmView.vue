<template>
  <v-container class="qcm-container" max-width="800">
    <v-card elevation="2" class="pa-6">
      <v-card-title class="text-h5 justify-center">QCM</v-card-title>

      <div class="mb-4">
        Question {{ currentIndex + 1 }} / {{ questions.length }}
      </div>

      <v-card class="pa-4 mb-4">
        <div class="text-subtitle-1 font-weight-medium mb-3">{{ questions[currentIndex].text }}</div>
        <v-radio-group v-model="answers[currentIndex]" mandatory>
          <v-radio
            v-for="(choice, i) in questions[currentIndex].choices"
            :key="i"
            :label="choice"
            :value="choice"
          />
        </v-radio-group>
      </v-card>

      <div class="d-flex justify-space-between">
        <v-btn text :disabled="currentIndex === 0" @click="prevQuestion">Précédent</v-btn>
        <v-btn
          color="primary"
          :disabled="!answers[currentIndex]"
          v-if="currentIndex < questions.length - 1"
          @click="nextQuestion"
        >
          Suivant
        </v-btn>

        <v-btn
          color="success"
          :disabled="answers.includes('')"
          v-if="currentIndex === questions.length - 1"
          @click="submitQcm"
        >
          Terminer
        </v-btn>
      </div>

      <div class="d-flex justify-end mt-3">
        <v-btn text @click="resetQcm">Réinitialiser</v-btn>
      </div>

      <v-alert
        v-if="score !== null"
        :type="score >= 70 ? 'success' : 'warning'"
        class="mt-4"
        border="left"
        colored-border
      >
        <strong>Résultat :</strong> {{ score }} % de bonnes réponses ({{ correct }}/{{ questions.length }})
      </v-alert>
    </v-card>
  </v-container>
</template>

<script>
export default {
  name: 'QcmView',
  data() {
    return {
      questions: [
        {
          text: 'Combien de points vaut un ippon au judo ?',
          choices: ['1', '2', '10', '100'],
          correct: '100'
        },
        {
          text: 'Quel est le terme pour un décompte de pénalité ?',
          choices: ['Waza-ari', 'Shido', 'Osae-komi', 'Yuko'],
          correct: 'Shido'
        },
        {
          text: 'Quelle couleur de ceinture est la plus élevée parmi celles-ci ?',
          choices: ['Jaune', 'Bleu', 'Vert', 'Noir'],
          correct: 'Noir'
        },
        {
          text: 'Comment s’appelle la prise de bras classique en judo ?',
          choices: ['Uchi-mata', 'Osoto-gari', 'Seoi-nage', 'Kouchi-gari'],
          correct: 'Seoi-nage'
        },
        {
          text: 'En compétition, quel est le temps maximum d’un combat senior ?',
          choices: ['2 min', '4 min', '5 min', '8 min'],
          correct: '4 min'
        }
      ],
      currentIndex: 0,
      answers: ['', '', '', '', ''],
      score: null,
      correct: 0
    }
  },
  methods: {
    nextQuestion() {
      if (!this.answers[this.currentIndex]) return
      if (this.currentIndex < this.questions.length - 1) {
        this.currentIndex += 1
      }
    },
    prevQuestion() {
      if (this.currentIndex > 0) {
        this.currentIndex -= 1
      }
    },
    submitQcm() {
      this.correct = this.questions.reduce((total, question, idx) => {
        return total + (this.answers[idx] === question.correct ? 1 : 0)
      }, 0)
      this.score = Math.round((this.correct / this.questions.length) * 100)
    },
    resetQcm() {
      this.answers = this.questions.map(() => '')
      this.currentIndex = 0
      this.score = null
      this.correct = 0
    }
  }
}
</script>

<style scoped>
.qcm-container {
  margin: 100px auto 40px;
}
</style>