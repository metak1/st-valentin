<template>
  <div class="container">
    <img
      src="/valentine.gif"
      alt="Valentine"
      class="gif"
    />

    <h1>
      Tu veux être ma valentine de noël du nouvel an du 14 février ? 💝
    </h1>

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

// ✅ Bouton reste à l'écran même en scale
const yesStyle = computed(() => {
  const buttonBaseWidth = 160; // largeur de base
  const buttonHeight = 60;     // hauteur de base
  const padding = 16;          // padding écran

  const scale = 1 + noClicks.value * 0.2;
  const buttonWidth = buttonBaseWidth * scale; // largeur réelle après scale

  if (noClicks.value < 2) {
    return {
      transform: `scale(${scale})`,
      position: "static"
    }
  }

  // Limites pour rester dans l'écran
  const maxX = Math.max(window.innerWidth - buttonWidth - padding, padding);
  const maxY = Math.max(window.innerHeight - buttonHeight - padding - 120, padding);

  return {
    position: "absolute",
    left: `${Math.random() * maxX}px`,
    top: `${Math.random() * maxY}px`,
    transform: `scale(${scale})`
  }
})

function onNo() {
  noClicks.value++
}

function sayYes() {
  accepted.value = true
}
</script>

<style scoped>
.container {
  min-height: 100svh;
  padding: 24px 16px;
  text-align: center;
  font-family: sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.gif {
  width: 160px;
  max-width: 70%;
  margin-bottom: 16px;
}

h1 {
  font-size: 1.2rem;
  max-width: 90%;
}

.buttons {
  margin-top: 24px;
  position: relative;
  width: 100%;
  max-width: 320px;
  height: 220px;
  display: flex;
  flex-direction: column;
  gap: 16px;
  align-items: center;
}

button {
  padding: 14px 20px;
  font-size: 1rem;
  border: none;
  border-radius: 14px;
  cursor: pointer;
  width: 100%;
  max-width: 240px;
}

.yes {
  background-color: #ff4d6d;
  color: white;
  transition: transform 0.3s ease, left 0.3s ease, top 0.3s ease;
}

.no {
  background-color: #ccc;
}

.success {
  margin-top: 24px;
  font-size: 1.6rem;
}

/* Desktop */
@media (min-width: 768px) {
  .gif {
    width: 200px;
  }

  h1 {
    font-size: 1.6rem;
  }

  .buttons {
    flex-direction: row;
    justify-content: center;
    height: 200px;
  }

  .no {
    margin-left: 20px;
  }
}
</style>
