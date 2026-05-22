<script setup lang="ts">
import Call from '@/assets/Call.png'
import Logo from '@/assets/Logo.png'
</script>

<template>
  <div class="flex items-center absolute left-0 right-0 top-0">
    <div class="ml-[205px] mt-[34px] w-[237px] h-[50.96px]">
      <img :src="Logo" alt="Logo">
    </div>
    <div class="flex gap-8 ml-[559px] text-[18px] items-center ">
      <span class="hover:text-[#CB3B48] hover:shadow-text-glow transition-all duration-300 cursor-pointer text-white mt-[15px]">Главная</span>
      <span class="hover:text-[#CB3B48] hover:shadow-text-glow transition-all duration-300 cursor-pointer text-white mt-[15px]">Меню</span>
      <span class="hover:text-[#CB3B48] hover:shadow-text-glow transition-all duration-300 cursor-pointer text-white mt-[15px]">Еще...</span>
      <button class="cursor-pointer ml-4 ">
        <img :src="Call" alt="Call" class="mt-[15px]">
      </button>
    </div>
    <div>
      <button class="bg-white w-[179px] h-[50px] rounded-xl mt-[15px] ml-[50px] text-[#CB3B48] text-[18px] font-medium hover:cursor-pointer">Забронировать</button>
    </div>
  </div>
</template>