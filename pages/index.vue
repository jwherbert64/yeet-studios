<template>
  <div class="app">
    <pads 
      :isRecording="isRecording"
      @triggered="handlePad" />
    <div>
    </div>
    <panel
      :recordEvents="recordEvents"
      :recordTime="recordTime"
      @triggered="handleRecord"
      @update="recordTime++" />
  </div>
</template>

<script>
  import Pads from '~/components/Pads.vue'
  import Panel from '~/components/Panel.vue'

  export default {
    components: {
      Pads,
      Panel
    },
    data() {
      return {
        recordEvents: [],
        isRecording: false,
        recordTime: 0
      }
    },
    methods: {
      handlePad(sourceUrl) {
        let recordEvent = {
          sourceUrl: sourceUrl,
          time: this.recordTime
        }

        this.recordEvents.push(recordEvent)
      },
      handleRecord(isRecording) {
        this.isRecording = isRecording

        if (this.isRecording) {
          this.recordEvents = []
          this.recordTime = 0
        }
      }
    }
  }
</script>

<style>
.app {
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>
