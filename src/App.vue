<template>
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
<h1 class="text-center">Super Quiz</h1>
<transition name="flip" mode="out-in">
<component :is="mode" @answered="answered($event)" @confirmed="mode = 'app-questions'"></component>
</transition>
</div>
</div>
</div>
</template>

<script>
import Answers from "./components/Answers";
import Questions from "./components/Questions";

export default {
  data() {
    return {
      mode: "app-questions"
    };
  },
  methods: {
    answered(isCorrect) {
      if (isCorrect) {
        this.mode = "app-answers";
      } else {
        this.mode = "app-questions";
        alert("Wrong Answer, Try Again");
      }
    }
  },
  components: {
    "app-answers": Answers,
    "app-questions": Questions
  }
};
</script>

<style>
.flip-enter-active {
  animation: flip-in 0.5s ease-in forwards;
}
.flip-leave-active {
  animation: flip-out 0.5s ease-in forwards;
}

@keyframes flip-out {
  from {
    transform: rotateY(0deg);
  }
  to {
    transform: rotateY(90deg);
  }
}

@keyframes flip-in {
  from {
    transform: rotateY(90deg);
  }
  to {
    transform: rotateY(0deg);
  }
}
</style>
