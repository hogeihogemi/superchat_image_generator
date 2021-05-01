<template>
  <div class="container">
    <SuperChat
      :content="state.content"
      :content-color="colorList[selectedPriceIndex].content"
      :header-color="colorList[selectedPriceIndex].header"
      :price="Number(state.price).toLocaleString()"
      :username="state.username"
      :iconUrl="state.iconUrl"
    />
    <div>
      <input v-model="state.iconUrl" class="border" />
      <input v-model="state.username" class="border" />
      <input v-model="state.content" class="border" />
      <select
        :value="state.price"
        @input="state.price = Number($event.target.value.replace(',', ''))"
      >
        <option v-for="color in colorList" :key="color.price">
          {{ color.price }}
        </option>
      </select>
      <button @click="savePng">save</button>
    </div>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, reactive } from '@nuxtjs/composition-api'
import SuperChat from '@/components/SuperChat.vue'
import domtoimage from 'dom-to-image'
import { saveAs } from 'file-saver'

export default defineComponent({
  components: {
    SuperChat,
  },
  setup() {
    const colorList = [
      {
        price: 200,
        content: 'rgba(0,229,255,1)',
        header: 'rgba(0,184,212,1)',
      },
      {
        price: 500,
        content: 'rgba(29,233,182,1)',
        header: 'rgba(0,191,165,1)',
      },
      {
        price: 1000,
        content: 'rgba(255,202,40,1)',
        header: 'rgba(255,179,0,1)',
      },
      {
        price: 2000,
        content: 'rgba(245,124,0,1)',
        header: 'rgba(230,81,0,1)',
      },
      {
        price: 5000,
        content: 'rgba(233,30,99,1)',
        header: 'rgba(194,24,91,1)',
      },
      {
        price: 10000,
        content: 'rgba(230,33,23,1)',
        header: 'rgba(208,0,0,1)',
      },
    ]

    const state = reactive({
      content: 'スパチャです！',
      price: 200,
      username: '???????',
      iconUrl: '',
    })
    const savePng = () => {
      domtoimage.toBlob(document.getElementById('card')).then(function (blob) {
        saveAs(blob, `superChat_${new Date().getTime()}.png`)
      })
    }

    const selectedPriceIndex = computed(() => {
      return colorList.findIndex((color) => color.price === state.price)
    })

    return {
      savePng,
      state,
      colorList,
      selectedPriceIndex,
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
