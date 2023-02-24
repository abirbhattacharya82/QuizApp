<template>
    <div class="Title">
        Quiz App
    </div>
    <div class="Subtitle" v-if="showC1">
        Click on the button below to start the Quiz
    </div>
    <button @click="start()" v-if="showC1">Start Quiz</button>
</template>

<script>
export default {
  data() 
  {
    return {
      showC1: true
    };
  },
  methods:
  {
    start()
    {
        this.show=false
    }
  }
}
</script>