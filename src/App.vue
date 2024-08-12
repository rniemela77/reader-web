<script setup>
import { ref, reactive, onMounted } from 'vue'

const mouse = reactive({ x: 0, y: 0 })

window.addEventListener('mousemove', (event) => {
  mouse.x = event.clientX
  mouse.y = event.clientY
})

// hiarchy ref
const hierarchy = ref(null)

// on mounted
onMounted(() => {
  // every 0.2s
  setInterval(() => {
    // get all the elements in the hierarchy
    const elements = hierarchy.value.children

    // find in % the x position of the mouse on the screen
    const mouseXPct = (mouse.x / window.innerWidth) * 100

    // loop through all the elements
    for (let i = 0; i < elements.length; i++) {
      // find in % the x position of the element on the screen
      const elementXPct = (elements[i].offsetLeft / window.innerWidth) * 100

      // find the distance between the mouse and the element
      const distance = Math.abs(mouseXPct - elementXPct)

      // find the scale (0.1 to 5)
      const scale = 1 + (1 - distance / 100) * 2

      // find the opacity
      const opacity = 1 - (distance / 100) * 10

      elements[i].style.transform = `scale(${scale})`
      elements[i].style.opacity = opacity
    }
  }, 300)
})
</script>

<template>
  <main ref="hierarchy">
    <h1>Organizing and Presenting</h1>
    <p>How you receive information matters</p>
    <h2>The Way You Read</h2>
    <p>Intentional Actions encourage Intentional Reading</p>
    <h2>Hierarchy is a way for ideas to relate to one another</h2>
    <p>All "highest level" go to the left. The start</p>
    <p>Branching roads appear, and more "littler" concepts arise out of the right</p>
  </main>
</template>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
* {
  transition: all 0.6s;
  transition-timing-function: cubic-bezier(0.5, 0.5, 0.5, 0.5);
  transform-origin: left center;
}
</style>
