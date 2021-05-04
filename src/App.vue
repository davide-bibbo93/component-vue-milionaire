<template>
  <div id="app">
        <div class="top">
            <img alt="logo" src="./assets/logo.png" height="200" />
        </div>
        <div class="content">
            <Question :qText="gameQuest.text" />
            <div class="answers">
                <div
                  v-for="ans in gameQuest.answers"
                  :key="ans"
                  ref="risposta"
                  @click="check($event, ans)"
                >
                  <Answer :aText="ans" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>

  import Question from "./components/Question";
  import Answer from "./components/Answer";

  export default {
    name: "App",
    components: {
      Question,
      Answer,
    },

  data() {
    return {
      questions: [
        {
          id: 1,
          text: "Che tipo di mostro era Cerbero?",
          answers: {
            a: "Un toro a 2 teste",
            b: "Un cane a 3 teste",
            c: "Un cane a 6 zampe",
            d: "Un drago a 9 code",
          },
          correctAns: "Un cane a 3 teste",
        },
        {
          id: 2,
          text: "Quale di queste affermazioni sulla balena è sbagliata?",
          answers: {
            a: "Possiede i fanoni",
            b: "E'un cetaceo",
            c: "Ha 2 piccoli alla volta",
            d: "Si nutre di krill",
          },
          correctAns: "Ha 2 piccoli alla volta",
        },
        {
          id: 3,
          text: "Quale è il vero cognome del famoso scrittore Alberto Moravia?",
          answers: {
            a: "Lanterni",
            b: "Pincherle",
            c: "Manterne",
            d: "Fincherni",
          },
          correctAns: "Pincherle",
        },
        {
          id: 4,
          text: "Come si chiamava la madre della Madonna?",
          answers: {
            a: "Anna",
            b: "Elisabetta",
            c: "Giuditta",
            d: "Maddalena",
          },
          correctAns: "Anna",
        },
        {
          id: 5,
          text: "Quale best seller di Stephen King si svolge in un grande hotel?",
          answers: {
            a: "Misery",
            b: "Shining",
            c: "Carrie",
            d: "Il miglio verde",
          },
          correctAns: "Shining",
        },
        {
          id: 6,
          text: "Chi è Edson Arantes do Nascimento?",
          answers: {
            a: "Ronaldo",
            b: "Pelè",
            c: "Serginho",
            d: "Falcao",
          },
          correctAns: "Pelè",
        },
      ],

      gameQuest: {},
      points: 0,

    };
  },

  methods: {

    check(event, answer) {
      const allAnswer = this.$refs.risposta;
      const clickedAnswer = allAnswer.filter(
        (risposta) => risposta.innerText == answer
      )[0];

      if (clickedAnswer.innerText == this.gameQuest.correctAns) {
        event.target.style.background = "green";
        this.points++;
      } else {
        event.target.style.background = "red";
      }

      // tolgo la domanda dall'array e aggiorno l'array
      const updatedQuestions = this.questions.filter(
        (question) => question != this.gameQuest
      );

      this.questions = updatedQuestions;
      // console.log(this.questions);

      // attendo e cambia la domanda, nel caso di domande finite esce un alert
      setTimeout(() => {
        if (this.questions.length == 0) {
          alert(
            `Gioco finito. Hai risposto correttamente a ${this.points} domande su 6.`
          );
          window.location.href = "/";
        } else {
          if (this.questions.length > 1) {
            this.randomQuest();
          } else {
            this.gameQuest = this.questions[0];
          }
        }
      }, 1000);

    },

    randomQuest() {
      const randIndex = Math.floor(Math.random() * this.questions.length);
      this.gameQuest = this.questions[randIndex];
    },

  },

  mounted() {
    this.randomQuest();
  },

};
</script>


<style lang="scss">

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    background: #12093a;
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  .top {
    width: 100%;
    padding: 1.5rem;
    background: rgb(58, 61, 180);
    display: grid;
    place-items: center;
  }

  .content {
    padding: 2rem;

    .answers {
      margin-top: 4rem;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 3rem;
    }

  }

  @media (max-width: 700px) {

    .content .answers {
      grid-template-columns: 1fr;
      gap: 2rem;
    }

  }

</style>