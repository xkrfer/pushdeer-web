<template>
  <div class="text-center mt-[24px]">
    <p>请用 ios14+ 系统摄像头扫码 然后输入以下URL进行测试</p>
    <p class="my-[12px]">
      <span class="bg-[#eb6c31] px-[12px] py-[6px] rounded-[8px] text-white">{{ origin }}</span>
    </p>
    <img src="/clip.png" alt="clip" class="mx-auto">
  </div>
</template>

<script setup lang="ts">
// @ts-ignore
import Cookies from 'js-cookie'
import {onMounted} from "vue";
const {origin} = window.location

const getCookie = () => {
  const token = Cookies.get("token")
  const customEvent = new CustomEvent('__PUSH_DEER_TOKEN__', {
    detail: {
      token
    }
  })
  document?.dispatchEvent(customEvent)
}


onMounted(() => {
  getCookie()
})

</script>
