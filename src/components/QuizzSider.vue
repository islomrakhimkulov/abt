<template>
  <aside class="quizz-sider" :class="{ 'quizz-sider--open': value }">
    <header class="quizz-sider__header">
      <button class="quizz-sider__btn" @click="toggleSider">
        <Icon v-if="!value" size="36">
          <ChevronLeftFilled />
        </Icon>
        <Icon v-else size="36">
          <ChevronRightFilled />
        </Icon>
      </button>
    </header>
    <div v-if="value">
      <div class="quizz-sider__content">
        <div class="quizz-sider__subject">
           <h2>Matematika</h2>
        </div>
        <div class="quizz-sider__total">
          <p>7/{{quizzes.length }}</p>
          
        </div>
      </div>
      
      <div v-for="quizz in quizzes" :key="quizz.id">
        <div class="quizz-sider__items" >
          {{ quizz.id }}
          <p>{{ quizz.userAnswer }}</p>
        </div>
      </div>
      
    </div>
  </aside>
</template>

<script>
import { Icon } from "@v2icons/utils";
import { ChevronLeftFilled, ChevronRightFilled } from "@v2icons/material";
export default {
  name: "QuizzSider",
  components: { Icon, ChevronLeftFilled, ChevronRightFilled },
  props: {
    value: {
      type: Boolean,
      default: false,
    },
    quizzes: {
      type: Array,
      default: () => ({}),
    }
  },
  data: () => ({
    quizzes: [],
    userAnswer: null,
  }),
  methods: {
    toggleSider() {
      this.$emit("input", !this.value);
    },
  },
};
</script>

<style lang="scss">
@import "@/assets/quizz.scss";
.quizz-sider {
  position: fixed;
  top: 0;
  right: 0;
  width: 65px;
  height: 100vh;
  background: $quizz-color;
  transition: width 0.5s;
  &__header {
    height: 56px;
    display: flex;
  }
  &__btn {
    background: darken($quizz-color, 5%);
    border: 0;
    cursor: pointer;
    width: 100%;
  }
  &--open {
    width: 530px;
    .quizz-sider__btn {
      width: 65px;
    }
  }
  &__items {
    display: flex;
    flex-direction: columns;
    border-radius: 50%;
    padding: 4px;
    margin-right: 15px;
  }
  &__content {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  &__subject {
    margin-left: 10px;
  }
  &__total {
    margin-right: 10px;
    font-weight: bolder;
  }
}

</style>