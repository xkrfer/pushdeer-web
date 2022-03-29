<template>
  <div class="text-center mt-[24px]">
    <p>请用 ios14+ 系统摄像头扫码 然后输入以下URL进行测试</p>
    <p class="my-[12px]">
      <span class="bg-[#eb6c31] px-[12px] py-[6px] rounded-[8px] text-white">{{ origin }}</span>
    </p>
    <img src="/clip.png" alt="clip" class="mx-auto">
    <div class="pt-[48px]" v-if="client_id">
      <span class="bg-[#3894ff] px-[12px] py-[6px] rounded-[8px] text-white cursor-pointer" @click="OAuthToGithub">Github登陆</span>
    </div>
  </div>
</template>


<script setup lang="ts">
// @ts-ignore
import Cookies from 'js-cookie'
const { origin } = window.location
const client_id = Cookies.get('github_client_id')
const OAuthToGithub = () => {
  if(client_id){
    window.location.href = `https://github.com/login/oauth/authorize?client_id=${client_id}&redirect_uri=${origin}/oauth/redirect/github`
  }
}

</script>
