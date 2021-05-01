<template>
  <div class="container mx-auto">
    <div class="form mb-4">
      <div class="flex mb-4">
        <div class="mr-4 w-3/12">
          <label for="screen_name"> ユーザー名 </label>
          <input id="screen_name" v-model="state.username" />
        </div>
        <div class="mr-4 w-2/12">
          <label for="price">金額</label>
          <select
            id="price"
            class="block w-full bg-gray-200 border border-gray-200 text-gray-700 py-2 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
            :value="state.price"
            @input="state.price = Number($event.target.value.replace(',', ''))"
          >
            <option v-for="color in colorList" :key="color.price">
              {{ color.price }}
            </option>
          </select>
        </div>
        <div class="w-7/12">
          <label for="icon_url"> アイコン画像URL </label>
          <input id="icon_url" placeholder="https://" v-model="state.iconUrl" />
        </div>
      </div>
      <div class="mb-4 w-full">
        <label for="screen_name"> メッセージ </label>
        <textarea v-model="state.content" />
      </div>
      <div class="mt-8 w-full">
        <button
          @click="savePng"
          class="mb-3 rounded-full w-full shadow bg-blue-500 px-4 py-2 text-white hover:bg-blue-400"
        >
          画像ダウンロード
        </button>
      </div>
    </div>
    <div class="flex justify-center">
      <SuperChat
        :content="state.content"
        :content-color="colorList[selectedPriceIndex].content"
        :header-color="colorList[selectedPriceIndex].header"
        :price="Number(state.price).toLocaleString()"
        :username="state.username"
        :iconUrl="state.iconUrl"
      />
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
label {
  @apply block text-gray-700 text-sm font-bold mb-2;
}
input,
textarea {
  @apply shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none;
}
</style>
