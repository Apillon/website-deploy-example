<template>
  <div class="container">
    <img :src="logoUrl" alt="Bouncing Logo" @load="initAnimation" @click="changeTrajectory" />
    <div class="input-container">
      <input v-model="inputUrl" type="url" placeholder="Enter image URL" />
      <button @click="updateLogoUrl">Update Logo</button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'BouncingLogo',
  setup() {
    const logoUrl = ref('https://apillon.io/images/logo.svg')
    const inputUrl = ref('')

    function updateLogoUrl() {
      if (inputUrl.value) {
        logoUrl.value = inputUrl.value
        inputUrl.value = ''
      }
    }
    let xSpeed = 2
    let ySpeed = 2

    function changeTrajectory() {
      console.log('click')
      // Generate random angle for new trajectory
      const angle = Math.random() * (2 * Math.PI)
      const speedFactor = 20

      // Update speeds based on the angle
      xSpeed = speedFactor * Math.cos(angle)
      ySpeed = speedFactor * Math.sin(angle)

      // Reset speeds to normal after a short duration
      setTimeout(() => {
        xSpeed = 2 * Math.sign(xSpeed)
        ySpeed = 2 * Math.sign(ySpeed)
      }, 500)
    }

    function initAnimation(event: Event) {
      const logo = event.target as HTMLImageElement
      let x = 0
      let y = 0

      function animate() {
        x += xSpeed
        y += ySpeed

        if (x + logo.clientWidth >= window.innerWidth) {
          x = window.innerWidth - logo.clientWidth
          xSpeed = -xSpeed
        } else if (x <= 0) {
          x = 0
          xSpeed = -xSpeed
        }

        if (y + logo.clientHeight >= window.innerHeight) {
          y = window.innerHeight - logo.clientHeight
          ySpeed = -ySpeed
        } else if (y <= 0) {
          y = 0
          ySpeed = -ySpeed
        }

        logo.style.transform = `translate(${x}px, ${y}px)`
        requestAnimationFrame(animate)
      }

      animate()
    }

    return { logoUrl, inputUrl, updateLogoUrl, initAnimation, changeTrajectory }
  }
})
</script>

<style scoped>
.container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

img {
  /* position: absolute; */
  max-width: 300px;
}

.input-container {
  position: fixed;
  bottom: 20px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

input {
  width: 300px;
  padding: 6px 12px;
  margin-right: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

button {
  padding: 6px 12px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}
</style>
