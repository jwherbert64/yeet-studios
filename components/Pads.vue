<template>
  <div>
    <pad
      :sourceUrl="'http://soundbible.com/mp3/Air Plane Ding-SoundBible.com-496729130.mp3'"
      @triggered="triggerPad" />
    <pad
      :sourceUrl="'http://soundbible.com/mp3/Elevator Ding-SoundBible.com-685385892.mp3'"
      @triggered="triggerPad" />
  </div>
</template>

<script>
  import Pad from '~/components/Pad'

  export default {
    components: {
      Pad
    },
    props: {
      isRecording: Boolean
    },
    methods: {
      triggerPad(sourceUrl) {
        let audioEvent = new Audio(sourceUrl)
        audioEvent.play()

        if (sourceUrl && this.isRecording) {
          this.$emit('triggered', sourceUrl)
        }
      }
    }
  }
</script>

<style>

</style>