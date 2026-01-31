<template>
  <div class="container">
    <img
      src="/valentine.gif"
      alt="Valentine"
      class="gif"
    />

    <h1>Tu veux être ma valentine de noël du nouvel an du 14 février ? 💝</h1>

    <div class="buttons">
      <button
        class="yes"
        :style="yesStyle"
        @click="sayYes"
      >
        {{ yesText }}
      </button>

      <button class="no" @click="onNo">
        Non 😢
      </button>
    </div>

    <p v-if="accepted" class="success">
      💖 YAAAY !!! 💖
    </p>
  </div>
</template>

<script setup>
import { ref, computed } from "vue"

const noClicks = ref(0)
const accepted = ref(false)

const yesTextList = [
  "Oui ❤️",
  "Non il faut cliquer ici !!!!!",
  "Stopli...",
  "Mimi va te croquer les pieds",
  "Tu me détestes"
]

const yesText = computed(() =>
  yesTextList[Math.min(noClicks.value, yesTextList.length - 1)]
)

const yesStyle = computed(() => ({
  transform: `scale(${1 + noClicks.value * 0.3})`,
  position: noClicks.value >= 2 ? "absolute" : "static",
  top: noClicks.value >= 2 ? `${Math.random() * 60 + 20}%` : "auto",
  left: noClicks.value >= 2 ? `${Math.random() * 60 + 20}%` : "auto"
}))

function onNo() {
  noClicks.value++
}

function sayYes() {
  accepted.value = true
}
</script>

<style scoped>
.container {
  height: 100vh;
  text-align: center;
  padding-top: 40px;
  font-family: sans-serif;
}

.gif {
  width: 200px;
  margin-bottom: 20px;
}

.buttons {
  margin-top: 30px;
  position: relative;
  height: 200px;
}

button {
  padding: 12px 24px;
  font-size: 18px;
  border: none;
  border-radius: 12px;
  cursor: pointer;
}

.yes {
  background-color: #ff4d6d;
  color: white;
  transition: all 0.3s ease;
}

.no {
  margin-left: 20px;
  background-color: #ccc;
}

.success {
  margin-top: 30px;
  font-size: 28px;
}
</style>
