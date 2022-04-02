<template>
  <div class="text-center mt-[24px]">
    <p>请用 ios14+ 系统摄像头扫码 然后输入以下URL进行测试</p>
    <p class="my-[12px]">
      <span class="bg-[#eb6c31] px-[12px] py-[6px] rounded-[8px] text-white">{{ origin }}</span>
    </p>
    <img src="/clip.png" alt="clip" class="mx-auto">
    <div class="pt-[48px]" v-if="github_client_id">
      <span class="bg-[#3894ff] px-[12px] py-[6px] rounded-[8px] text-white cursor-pointer" @click="OAuthToGithub">Github登陆</span>
    </div>
  </div>
</template>


<script setup lang="ts">
// @ts-ignore
import Cookies from 'js-cookie'
import {onMounted, ref} from "vue";

const {origin} = window.location
const github_client_id = ref()
const OAuthToGithub = () => {
  if (github_client_id.value) {
    window.location.href = `https://github.com/login/oauth/authorize?client_id=${github_client_id.value}&redirect_uri=${origin}/login/github`
  }
}

const fetchAppId = async () => {
  const res = await fetch("/appid")
  const data = await res.clone().json()
  if (data.code === 0) {
    github_client_id.value = data.content.github
  }
}


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
  fetchAppId()
  getCookie()
})

</script>
