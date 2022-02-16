<template>
  <div class="quizz" :class="{ 'quizz--sider-open': isSiderOpen }">
    <main class="quizz__main">
      <header class="quizz__header">Matematika</header>
      <div class="quizz__content">
        <QuizzItem
          v-for="(quizz, index) in quizzes"
          :key="quizz.id"
          :quizz="quizz"
          :index="index + 1"
          @user-answer-change="handleUserAnswerChange"
        />
      </div>
      <div class="quizz__modal-content" v-if="openModal">
        <button @click="finishTest" class="quizz__button">Testni yakunlash</button>
      </div>
    </main>
    <QuizzSider
       :quizzes="quizzes"
       v-model="isSiderOpen"
    />
    
  </div>
</template>

<script>
import QuizzSider from "./QuizzSider.vue";
import QuizzItem from "./QuizzItem";
export default {
  name: "QuizzApp",
  components: { QuizzSider, QuizzItem },
  data() {
    return {
      isSiderOpen: false,
      quizzes: [
        {
          id: 1,
          question: "Quyidagi ko'paytmalardan qaysi biri 45 ga qoldiqsiz bo'linadi?",
          options: ["39⋅18", "234⋅80", "35⋅61", "80⋅23"],
          correctAnswer: "234⋅80",
          // userAnswer: "39⋅18",
        },
        {
          id: 2,
          question:
            "821 ga qanday eng kichik musbat sonni qo'shganda, yig'indi 66 ga qoldiqsiz bo‘linadi?",
          options: ["4", "7", "5", "1"],
          correctAnswer: "7",
        },
        {
          id: 3,
          question:
            "246*013579246∗013579 soni 99 ga bo'linishi uchun yulduzchaning o'rniga qanday raqam qo‘yilishi kerak?",
          options: ["8", "7", "0", "4"],
          correctAnswer: "8",
        },
        {
          id: 4,
          question:
            "nn raqamining qanday qiymatlarida 7851n7851n soni 99 ga qoldiqsiz bo‘linadi?",
          options: ["9", "4", "2", "6"],
          correctAnswer: "4",
        },
        {
          id: 5,
          question:
            "246*013579246*013579 soni 99 ga bo'linishi uchun yulduzchaning o‘rniga qanday raqam qo‘yilishi kerak?",
          options: ["8", "7", "0", "4"],
          correctAnswer: "8",
        },
        {
          id: 6,
          question:
            "821821 ga qanday eng kichik musbat sonni qo'shganda, yig'indi 66 ga qoldiqsiz bo‘linadi?",
          options: ["1", "4", "5", "7"],
          correctAnswer: "4",
        },
        {
          id: 7,
          question:
            "4*10 yozuvdagi yulduzchani shunday raqam bilan almashtiringki, hosil bo‘lgan son 4545 ga qoldiqsiz bo‘linsin.",
          options: ["6", "5", "4", "0"],
          correctAnswer: "4",
        },
        {
          id: 8,
          question:
            "821821 ga qanday eng kichik musbat sonni qo'shganda, yig'indi 66 ga qoldiqsiz bo‘linadi?",
          options: ["1", "4", "5", "7"],
          correctAnswer: "4",
        },
        {
          id: 9,
          question:
            "1782751617827516 quyidagi sonlardan qaysi biriga qoldiqsiz bo'linadi?",
          options: ["5", "10", "3", "4"],
          correctAnswer: "3",
        },
        {
          id: 10,
          question:
            "4*10 yozuvdagi yulduzchani shunday raqam bilan almashtiringki, hosil bo‘lgan son 4545 ga qoldiqsiz bo‘linsin",
          options: ["0", "4", "6", "5"],
          correctAnswer: "4",
        },
      ],
    };
  },
  computed: {
    openModal() {
      return this.quizzes.filter(item => item.userAnswer).length >= this.quizzes.length ;
    }
  }, 
  methods: {
    handleUserAnswerChange(data) {
      this.quizzes = this.quizzes.map((quizz) => {
        if (quizz.id === data.id) {
          return { ...quizz, userAnswer: data.answer };
        } else {
          return quizz;
        }
      });
    },
    finishTest() {
      console.log('sayHi')
      this.quizzes.userAnswer = '';
    }
  },
};
</script>

<style lang="scss">
.quizz {
  .quizz__main {
    width: calc(100% - 65px);
    transition: width 0.5s;
  }
  &--sider-open {
    .quizz__main {
      width: calc(100% - 530px);
    }
  }
  &__header {
    text-align: center;
    height: 56px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-bottom: 2px solid rgba(87, 87, 87, 0.12);
  }
  &__content {
    width: 80%;
    margin: 0 auto;
  }
  &__modal-content {
      
      width: 100%;
      padding: 100px 0;
      text-align: center;
      background: #333;
    }
    &__button {
      text-align: center;
      background: green;
      padding: 10px 15px;
      color: #fff;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
}
</style>