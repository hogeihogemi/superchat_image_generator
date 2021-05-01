<template>
  <div id="card" class="rounded">
    <div class="header flex rounded-t py-2 px-4">
      <img
        src="@/assets/hogemi_superchat.jpg"
        class="icon mr-4 rounded-full h-10 w-10 flex items-center justify-center"
      />
      <div class="text-left">
        <div class="username">ほげいほげみ</div>
        <div class="price">¥200</div>
      </div>
    </div>
    <div class="content rounded-b text-left py-2 px-4">{{ props.content }}</div>
  </div>
</template>

<script>
import { defineComponent } from '@nuxtjs/composition-api'
export default defineComponent({
  props: {
    content: {},
  },
  setup(props) {
    return {
      props,
    }
  },
})
</script>

<style lang="scss" scoped>
.header {
  background-color: #00b8d4;
  width: 579px;
  height: 56px;
}
.content {
  background-color: #00e5ff;
  width: 579px;
  height: 40px;
  font-size: 13px;
}
.username {
  color: #000000b3;
  font-size: 14px;
}
.price {
  font-weight: 500;
}
</style>
