<template>
  <div
    class="bg-gradient-to-b from-[#ffafbd] to-[#ffc3a0] flex justify-center items-center h-svh"
  >

    <div v-if="!isLetterOpened" class="cursor-pointer" @click="openLetter()">
      <img :src="LoveLetter" alt="click here" width="200" height="100" class="object-contain">
    </div>

    <div v-if="isCardOpen" class="bg-white p-6 rounded-2xl shadow-lg w-full text-center mx-2 my-5">
      <h2 class="text-2xl font-medium mb-4">💖 Happy 1st Anniversary 💖</h2>
      <p class="text-lg font-light mb-4">
        To my dearest, <strong>Kitty</strong> 🐱
      </p>
      <div class="w-[300px] h-[300px] mx-auto bg-[#ffafbd] rounded-lg p-2">
        <img
          :src="currentImage"
          alt="Happy Anniversary"
          width="300"
          height="300"
          class="rounded-lg object-cover aspect-square"
        />
      </div>
      <div v-if="isLoading" class="my-4">
        <div class="loading-spinner"></div>
      </div>
      <div v-if="!isLoading" class="my-4">
        <iframe
          style="border-radius: 12px"
          :src="currentTrackUri"
          width="100%"
          height="80"
          frameborder="0"
          allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"
          loading="lazy"
        ></iframe>
      </div>
      <div v-for="(card, index) in cards" :key="index" v-show="currentCard === index" class="mt-4">
        <div class="card bg-pink-100 p-4 rounded-lg shadow-md min-h-20">
          <p class="whitespace-pre-line">{{ card.text }}</p>
          <p class="text-center text-xs text-gray-500 font-light mt-2">{{ currentCard + 1 }}/{{ cards.length }}</p>
        </div>
        <div class="mt-4">
          <button
            v-if="index > 0"
            @click="prevCard"
            class="back-button bg-pink-500 text-white py-2 px-4 rounded-full mr-2 hover:bg-pink-600"
          >
            Back
          </button>
          <button
            v-if="index < cards.length - 1"
            @click="nextCard"
            class="next-button bg-pink-500 text-white py-2 px-4 rounded-full hover:bg-pink-600"
          >
            Next ❤️
          </button>
          <button
            v-if="index === cards.length - 1"
            class="next-button bg-green-500 text-white py-2 px-4 rounded-full hover:bg-green-600"
            @click="lastCard"
          >
            Next 💝
          </button>
        </div>
      </div>
    </div>

    <div v-if="isSummaryOpen" class="bg-white p-6 rounded-2xl shadow-lg w-full text-center mx-2 my-5">
      <h2 class="text-2xl font-medium mb-4">💖 in 2025 💖</h2>
      <p class="text-lg font-light ">
        <span>ปีนี้เราก็มาตั้งใจรักกันต่อไปงับ</span> 🥰
      </p>
      <p class="text-sm font-light mb-4">
        <span>by <strong>มิวแฟนสุดที่รักของคิตตี้</strong> 🐱</span>
      </p>
      <div class="w-[300px] h-[300px] mx-auto bg-[#ffafbd] rounded-lg p-2">
        <img
          src="https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExcmNzaW83ZmxqenpqZXZzdHNvdmh2NDVjZXdtdmppNnN2cW85bmdqYyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/wTQTQikaZmg59efFWh/giphy.gif"
          alt="Happy Anniversary"
          width="300"
          height="300"
          class="rounded-lg object-cover aspect-square"
        />
      </div>
      <div class="card bg-pink-100 p-4 rounded-lg shadow-md min-h-20 mt-4">
        <p class="whitespace-pre-line">{{ summaryText }}</p>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { onMounted, ref } from 'vue'
import LoveLetter from '@/assets/images/love-letter.svg'
import Month1 from '@/assets/images/month_1.webp'
import Month2 from '@/assets/images/month_2.png'
import Month3 from '@/assets/images/month_3.png'
import Month4 from '@/assets/images/month_4.webp'
import Month5 from '@/assets/images/month_5.png'
import Month6 from '@/assets/images/month_6.webp'
import Month7 from '@/assets/images/month_7.png'
import Month8 from '@/assets/images/month_8.png'
import Month9 from '@/assets/images/month_9.png'
import Month10 from '@/assets/images/month_10.png'
import Month11 from '@/assets/images/month_11.png'
import Month12 from '@/assets/images/month_12.png'

const isLetterOpened = ref(false)
const isCardOpen = ref(false)
const isSummaryOpen = ref(false)
const currentCard = ref(0)
const currentImage = ref('')
const currentTrackUri = ref('')
const isLoading = ref(true)
const cards = ref([
  {
    title: 'I Got you',
    text: '"No matter what, you got me, I got you \nAnd I wouldn\'t want it any other way"',
    track: 'https://open.spotify.com/embed/track/0mgveJEIGjcN51w4JIQtI6?utm_source=generator',
    image: Month1
  },
  {
    title: 'Really like you',
    text: '"말하고 싶어 To say I love you But girl,\nI like you Really, really like you"',
    track: 'https://open.spotify.com/embed/track/3entdIWiOuQfcXIkJEABsV?utm_source=generator',
    image: Month2
  },
  {
    title: 'Xoxo',
    text: '"Gimme X-O-X-O"',
    track: 'https://open.spotify.com/embed/track/5jJgfoe8qJ59Dtp5nWmVVX?utm_source=generator',
    image: Month3
  },
  {
    title: 'Dreams Come True',
    text: '"Funny how all dreams come true"',
    track: 'https://open.spotify.com/embed/track/2GyZkPeiJXXBqYY1ddtsjk?utm_source=generator',
    image: Month4
  },
  {
    title: 'Baby Blue Love',
    text: '"You\'re my baby blue love"',
    track: 'https://open.spotify.com/embed/track/7Jzo3IObpANz6giPTUrihB?utm_source=generator',
    image: Month5
  },
  {
    title: 'Day 1',
    text: '"Kiss kiss kiss 단 하루도 빼먹지 말고\nLove love love 잠들기 전 꼭 속삭여줘"',
    track: 'https://open.spotify.com/embed/track/74muMkVdMYoR65lhmdzy13?utm_source=generator',
    image: Month6
  },
  {
    title: 'NO PROBLEM',
    text: '"No,there ain\'t no problem For love"',
    track: 'https://open.spotify.com/embed/track/4zHvWi4iFAG45lgiN7smLC?utm_source=generator',
    image: Month7
  },
  {
    title: 'Hot Air Ballon',
    text: '"🎈"',
    track: 'https://open.spotify.com/embed/track/1mdtLny0zugh89vokWGG80?utm_source=generator',
    image: Month8
  },
  {
    title: 'DM',
    text: '"Doesn\'t matter\n특별한 me and you"',
    track: 'https://open.spotify.com/embed/track/7B9W7Qsy5M2kyUNjQYIEG8?utm_source=generator',
    image: Month9
  },
  {
    title: 'MIROH',
    text: '"뛰어든 건 나니까 I’m okay 👌"',
    track: 'https://open.spotify.com/embed/track/2sFWzfV3kqAwXEWM9BjzwH?utm_source=generator',
    image: Month10
  },
  {
    title: 'The Feels',
    text: '"You have stolen my heart, oh yeah\nNever let it go, oh oh no"',
    track: 'https://open.spotify.com/embed/track/1utDFK1ARQcuZSwapf3cfb?utm_source=generator',
    image: Month11
  },
  {
    title: 'Feel Special',
    text: '"You make me feel special ✨"',
    track: 'https://open.spotify.com/embed/track/3Hz3tTQwOdM6XkA0ALB2G9?utm_source=generator',
    image: Month12
  },
])
const summaryText = ref('just wanna see you more happier this year 💖')

const openLetter = () => {
  isLetterOpened.value = true
  isCardOpen.value = true
}

const nextCard = () => {
  if (currentCard.value < cards.value.length) {
    currentCard.value++
    loadCurrentImage()
    loadSpotifyIframe()
  }
}

const prevCard = () => {
  if (currentCard.value > 0) {
    currentCard.value--
    loadCurrentImage()
    loadSpotifyIframe()
  }
}

const lastCard = () => {
  isCardOpen.value = false
  currentCard.value = 0
  isSummaryOpen.value = true
}

const loadSpotifyIframe = () => {
  isLoading.value = true
  currentTrackUri.value = cards.value[currentCard.value].track

   //Wait for iframe to load
  setTimeout(() => {
    isLoading.value = false
  }, 100)
}

const loadCurrentImage = () => {
  currentImage.value = cards.value[currentCard.value].image
}

onMounted(() => {
  loadCurrentImage()
  loadSpotifyIframe()
})
</script>

<style scoped>
@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.loading-spinner {
  border: 8px solid rgba(0, 0, 0, 0.1);
  border-top: 8px solid #3498db;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  animation: spin 1s linear infinite;
  margin: auto;
}
</style>
