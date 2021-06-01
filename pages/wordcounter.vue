<template>
  <section class="section">
    <h2 class="title has-text-centered is-half has-text-grey">
      "Let's count the words!"
    </h2>
    <div class="columns is-centered">
      <div class="control column is-8">
        <textarea
          v-model="text"
          class="textarea has-fixed-size text-counter"
          placeholder="Fixed size textarea"
          @keypress="handleKeyPressed"
          @keyup.ctrl.enter="stopTimer"
        />
      </div>
    </div>
    <div class="columns is-centered">
      <div class="column is-8">
        <nav class="level">
          <div class="level-item has-text-centered">
            <div>
              <p class="heading">Letters</p>
              <p class="title">
                {{ letters }}
              </p>
            </div>
          </div>
          <div class="level-item has-text-centered">
            <div>
              <p class="heading">Words</p>
              <p class="title">
                {{ words }}
              </p>
            </div>
          </div>
          <div class="level-item has-text-centered">
            <div>
              <p class="heading">Time</p>
              <p class="title">
                {{ formattedTime }}
              </p>
            </div>
          </div>
        </nav>
      </div>
    </div>
    <div class="is-flex is-justify-content-center is-align-content-center">
      <div class="buttons is-justify-content-center">
        <b-button
          type="is-success"
          icon-left="timer"
          :disabled="timeInterval"
          class="m-1"
          @click="startTimer"
        >
          Start Timer
        </b-button>
        <b-button
          type="is-danger"
          icon-left="close-circle"
          :disabled="!timeInterval"
          class="m-1"
          @click="stopTimer"
        >
          Stop Timer
        </b-button>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      text: '',
      timePassed: 0,
      timeInterval: null,
    }
  },
  computed: {
    letters() {
      return this.text.length
    },
    words() {
      return this.text.split(' ').length - 1
    },
    formattedTime() {
      const timePassed = this.timePassed
      const minutes = Math.floor(timePassed / 60)
      let seconds = timePassed % 60

      if (seconds < 10) {
        seconds = `0${seconds}`
      }

      return `${minutes}:${seconds}`
    },
  },
  methods: {
    startTimer() {
      if (!this.timeInterval) {
        this.timePassed = 0
        this.text = ''
        this.timeInterval = setInterval(() => (this.timePassed += 1), 1000)
      }
    },
    stopTimer() {
      clearInterval(this.timeInterval)
      this.timeInterval = null
    },
    handleKeyPressed() {
      if (this.text.length === 0) {
        this.startTimer()
      }
    },
  },
}
</script>

<style lang="scss">
.text-counter {
  height: 200px;
}
</style>
