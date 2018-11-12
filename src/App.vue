<template>
  <div class="training">
    <h1>Math training</h1>
    <AppStartScreen
      v-if="state === 'start'"
      @onStart="onStart"
      ></AppStartScreen>
    <AppQuestion
      v-else-if="state === 'question'"
      @success="onSuccess"
      @error="onError"
    ></AppQuestion>
    <AppMessage
      v-else-if="state === 'message'"
      :type="message.type"
      :text="message.text"
      @onNext="onNext"
      ></AppMessage>
    <AppResultScreen v-else-if="state === 'result'"></AppResultScreen>
    <div v-else>Unknown state</div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      state: 'start',
      message: {
        type: '',
        text: ''
      }
    }
  },
  methods: {
    onStart(){
      this.state = 'question'
    },
    onSuccess() {
      this.state = 'message';
      this.message.text = 'Good Job!';
      this.message.type = 'success';
    },
    onError(msg) {
      this.state = 'message';
      this.message.text = msg;
      this.message.type = 'warning';
    },
    onNext() {
      this.state = 'question';
    }
  }
}
</script>

<style scoped>
.training {
  max-width: 700px;
  margin: 20px auto;
  ;
}
</style>
