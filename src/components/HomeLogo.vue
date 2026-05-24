<script setup>
import Kiss from '@/assets/kiss.png'
import nightClubHome from '@/assets/night-clubHome.png'
import Spent from '@/assets/SpentHome.png'
</script>

<template>
  <div class="flex items-center justify-center pt-38">
    <img :src="Spent" alt="Spent" class="animate-fade-in">

    <div class="absolute pt-100">
      <img :src="Kiss" alt="Kiss" class="animate-fade-in-up">
    </div>
    <div class ="absolute ml-[750px] mt-[160px]">
      <img :src="nightClubHome" alt="" class="animate-fade-in-right">
    </div>
  </div>

  <div class="flex items-center gap-20 pt-60 ml-[535px] mt-[30px] ">
    <button class="w-[385.5px] h-[74px] bg-[#CB3B48] text-[#FFFFFF] rounded-[7.4px] text-[23px] animate-fade-in-up cursor-pointer" style="animation-delay: 0.01s">Забронировать Столик</button>
    <button class="w-[385.5px] h-[74px] bg-[#FFFFFF] text-[#CB3B48] rounded-[7.4px] text-[23px] animate-fade-in-up cursor-pointer" style="animation-delay: 0.01s">Посмотреть меню</button>
  </div>
</template>

<style>
/* Добавьте это в ваш глобальный CSS файл (например, main.css или в тег style без scoped) */
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes fadeInRight {
  from {
    opacity: 0;
    transform: translateX(30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.animate-fade-in {
  animation: fadeIn 0.8s ease-out forwards;
}

.animate-fade-in-up {
  animation: fadeInUp 0.8s ease-out forwards;
}

.animate-fade-in-right {
  animation: fadeInRight 0.8s ease-out forwards;
}
</style>