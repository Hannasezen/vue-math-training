<template>
  <div class="training">
    <h1>Math training</h1>
    <div class="progress">
      <div class="progress-bar"></div>
    </div>
    <div class="box">
      <transition name="flip" mode="out-in">
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
      </transition>
    </div>
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
      },
      stats: {
        success: 0,
        error: 0
      },
      questMax: 3
    }
  },
  computed: {
    questDone() {
      return this.stats.success + this.stats.error;
    }
  },
  methods: {
    onStart(){
      this.state = 'question';
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
}

.box {
  margin: 10px 0;
}

.flip-enter {

}

.flip-enter-active {
  animation: flipInX 0.3s linear;
}

.flip-leave {

}

.flip-leave-active {
  animation: flipOutX 0.3s linear;
}

@keyframes flipInX {
  from{transform: rotateX(90deg);}
  to{transform: rotateX(0deg)}
}

@keyframes flipOutX {
  from{transform: rotateX(0deg);}
  to{transform: rotateX(90deg)}
}

</style>
