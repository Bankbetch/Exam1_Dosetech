<template>
  <div class="container">
    <button class="greeting-button" @click="onCLick">Good Morning</button>
    <button class="greeting-button" @click="onCLick">Good Afternoon</button>
    <button class="greeting-button" @click="onCLick">Good Night</button>
    <button class="dont-click-me">Don’t Click Me</button>
    <div
      class="question-section"
      v-for="(item, index) in renderQuestion"
      :key="index"
    >
      <b-form-group :label="item.question" v-slot="{ ariaDescribedby }">
        <span
          class="text-danger"
          v-if="
            !checkAnswer(item.selected, item.answers, item.correctAnswer) &&
              item.selected
          "
        >
          Correct answer is ({{ item.correctAnswer }})
        </span>
        <b-form-radio-group
          v-model="item.selected"
          :options="item.answers"
          :aria-describedby="ariaDescribedby"
          stacked
        ></b-form-radio-group>
      </b-form-group>
    </div>
    <button @click="checkUserAnswerAllQuestion">
      checkUserAnswerAllQuestion
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      myQuestions: [
        {
          question: "1 + 2 is ?",
          answers: ["1", "2", "3"],
          correctAnswer: 2,
          selected: undefined
        },
        {
          question: "What is the best site for Web Programmer ?",
          answers: ["Stack Overflow", "Quora", "w3school"],
          correctAnswer: 0,
          selected: undefined
        },
        {
          question: "Who is Prime minister fo Thailand ?",
          answers: [
            "Prayut Chan-o-cha",
            "Yingluck Shinawatra",
            "Abhisit Vejjajiva",
            "Somchai Wongsawat"
          ],
          correctAnswer: 0,
          selected: undefined
        }
      ]
    };
  },
  computed: {
    renderQuestion() {
      return this.myQuestions;
    }
  },
  methods: {
    onCLick() {
      alert("Hint : $(‘.greeting-button’)");
    },
    checkAnswer(selected, data, correctAnswer) {
      return correctAnswer === data.indexOf(selected);
    },
    checkUserAnswerAllQuestion() {
      this.myQuestions.forEach((element, index) => {
        if (!element.selected)
          alert(`You have not answered question ${index + 1} `);
      });
    }
  }
};
</script>

<style></style>
