<template>
  <div class="container">
    <SuperChat />
    <button @click="savePng">save</button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from '@nuxtjs/composition-api'
import SuperChat from '@/components/SuperChat.vue'
import domtoimage from 'dom-to-image'
import { saveAs } from 'file-saver'

export default defineComponent({
  components: {
    SuperChat,
  },
  setup() {
    const savePng = () => {
      domtoimage.toBlob(document.getElementById('card')).then(function (blob) {
        saveAs(blob, `superChat_${new Date().getTime()}.png`)
      })
    }
    return {
      savePng,
    }
  },
})
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
