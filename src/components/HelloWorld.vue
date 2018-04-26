<template>
  <div class="hello">
    hello hiho!
    <button @click="startRecord">start!</button>
    <button @click="stopRecord">stop!</button>
    <audio controls id="audio"></audio>
  </div>
</template>

<script>
export default {
  data () {
    return {
      stream: null,
      mediaRecorder: null
    }
  },

  mounted () {
    navigator.mediaDevices.getUserMedia({audio: true, video: false})
      .then((stream) => {
        this.stream = stream
        this.mediaRecorder = new MediaRecorder(stream)
        this.mediaRecorder.ondataavailable = this.onFinishedReocrd
      })
  },

  methods: {
    startRecord () {
      this.mediaRecorder.start()
    },

    stopRecord () {
      this.mediaRecorder.stop()
    },

    onFinishedReocrd (event) {
      const audio = document.getElementById('audio')
      audio.setAttribute('controls', '')
      const audioURL = window.URL.createObjectURL(event.data)
      audio.src = audioURL
    }
  }
}
</script>
