<template>
  <div>
    <div
      class="record"
      v-if="!isPlaying"
      @click="triggerRecord">
      Record
    </div>
    <div 
      class="play"
      v-if="!isRecording"
      @click="triggerPlay">
      Play
    </div>
    <div
      class="stop"
      v-if="!isRecording"
      @click="triggerStop">
      Stop
    </div>
    <span>
      {{ playTime }}
    </span>
    <span>
      {{ recordTime }}
    </span>
    <input
      id="time-range"
      v-if="!isRecording"
      type="range"
      min="0"
      v-bind:max="recordTime"
      v-bind:value="playTime"
      @change="triggerTime">
  </div>
</template>

<script>
  export default {
    props: {
      recordEvents: Array,
      recordTime: Number
    },
    data() {
      return {
        interval: null,
        playTime: 0,
        isRecording: false,
        isPlaying: false,
        eventsIndex: 0
      }
    },
    methods: {
      triggerRecord() {
        if (this.isRecording) {
          this.isRecording = false
          this.$emit('triggered', this.isRecording)
          clearInterval(this.interval)
        } else {
          this.isRecording = true
          this.$emit('triggered', this.isRecording)
          this.interval = setInterval(this.updateRecordTime, 1000)
        }
      },
      triggerPlay() {
        if (this.playTime === this.recordTime) {
          this.playTime = 0
        }

        if (this.isPlaying === true) {
          clearInterval(this.interval)
        }

        this.isPlaying = true
        this.interval = setInterval(this.handlePlayEvent, 1000)
      },
      triggerStop() {
        this.playTime = 0
        this.isPlaying = false
        clearInterval(this.interval)
      },
      triggerTime() {
        this.playTime = Number(document.getElementById("time-range").value)
      },
      updateRecordTime() {
        this.$emit('update')
      },
      handlePlayEvent() {
        this.playTime += 1

        if (this.recordEvents[this.eventsIndex] && this.playTime === this.recordEvents[this.eventsIndex].time) {
          let audioEvent = new Audio(this.recordEvents[this.eventsIndex].sourceUrl)
          audioEvent.play()
          this.eventsIndex += 1
        }

        if (this.playTime === this.recordTime) {
          this.eventsIndex = 0
          this.isPlaying = false
          clearInterval(this.interval)
        }
      }
    }
  }
</script>