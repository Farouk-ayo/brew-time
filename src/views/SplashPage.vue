<template>
  <div class="relative min-h-screen w-full overflow-hidden bg-brew-dark">
    <canvas ref="webglCanvas" class="absolute inset-0 z-5"></canvas>

    <div class="absolute inset-0 z-0">
      <img
        src="@/assets/images/bg-coffee-shop.png"
        alt="Coffee Shop"
        class="w-full h-full object-cover"
      />
      <div class="absolute inset-0 bg-black/65"></div>
    </div>

    <div
      class="absolute -top-20 left-0 right-0 h-16 md:h-24 lg:h-48 overflow-hidden z-0 opacity-10"
    >
      <div ref="topScroll" class="flex gap-6 md:gap-12 whitespace-nowrap">
        <img
          v-for="i in 20"
          :key="i"
          src="@/assets/icons/brewtime-outline.svg"
          alt=""
          class="h-14 md:h-20 lg:h-48 w-auto shrink-0"
        />
      </div>
    </div>

    <div
      class="absolute -bottom-20 left-0 right-0 h-16 md:h-24 lg:h-48 overflow-hidden z-0 opacity-10"
    >
      <div ref="bottomScroll" class="flex gap-6 md:gap-12 whitespace-nowrap">
        <img
          v-for="i in 20"
          :key="i"
          src="@/assets/icons/brewtime-outline.svg"
          alt=""
          class="h-14 md:h-20 lg:h-48 w-auto shrink-0"
        />
      </div>
    </div>

    <div
      class="relative z-10 flex flex-col items-center justify-center min-h-screen px-4 py-8 gap-6 md:gap-12 lg:gap-16"
    >
      <div ref="logoRef">
        <img src="@/assets/icons/brewtime.svg" alt="BrewTime" class="w-48 md:w-80 lg:w-md h-auto" />
      </div>

      <div ref="creditsRef" class="flex items-center gap-4 md:gap-8 lg:gap-12 text-white">
        <div class="hidden md:block w-16 lg:w-24 h-px bg-white/30"></div>
        <img
          src="@/assets/icons/rage-media.svg"
          alt="Rage Media"
          class="h-10 md:h-14 lg:h-16 w-auto"
        />
        <div class="hidden md:block w-16 lg:w-24 h-px bg-white/30"></div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'
import * as THREE from 'three'

const logoRef = ref<HTMLElement | null>(null)
const creditsRef = ref<HTMLElement | null>(null)
const topScroll = ref<HTMLElement | null>(null)
const bottomScroll = ref<HTMLElement | null>(null)
const webglCanvas = ref<HTMLCanvasElement | null>(null)

let topAnimation: number | null = null
let bottomAnimation: number | null = null
let scene: THREE.Scene | null = null
let camera: THREE.PerspectiveCamera | null = null
let renderer: THREE.WebGLRenderer | null = null
let particles1: THREE.Points | null = null
let particles2: THREE.Points | null = null
let animationId: number | null = null

const initParticles = () => {
  if (!webglCanvas.value) return

  scene = new THREE.Scene()

  camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
  camera.position.z = 5

  renderer = new THREE.WebGLRenderer({
    canvas: webglCanvas.value,
    alpha: true,
    antialias: true,
  })
  renderer.setSize(window.innerWidth, window.innerHeight)
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))

  const particleCount = 100

  const positions1 = new Float32Array(particleCount * 3)
  const velocities1 = new Float32Array(particleCount * 3)

  for (let i = 0; i < particleCount; i++) {
    positions1[i * 3] = (Math.random() - 0.5) * 15
    positions1[i * 3 + 1] = Math.random() * 10 - 5
    positions1[i * 3 + 2] = (Math.random() - 0.5) * 10

    velocities1[i * 3] = (Math.random() - 0.5) * 0.02
    velocities1[i * 3 + 1] = Math.random() * 0.02 + 0.01
    velocities1[i * 3 + 2] = (Math.random() - 0.5) * 0.02
  }

  const geometry1 = new THREE.BufferGeometry()
  geometry1.setAttribute('position', new THREE.BufferAttribute(positions1, 3))

  const material1 = new THREE.PointsMaterial({
    color: 0x5e361c,
    size: 0.05,
    transparent: true,
    opacity: 0.6,
    blending: THREE.AdditiveBlending,
  })

  particles1 = new THREE.Points(geometry1, material1)
  scene.add(particles1)
  particles1.userData.velocities = velocities1

  const positions2 = new Float32Array(particleCount * 3)
  const velocities2 = new Float32Array(particleCount * 3)

  for (let i = 0; i < particleCount; i++) {
    positions2[i * 3] = (Math.random() - 0.5) * 15
    positions2[i * 3 + 1] = Math.random() * 10 - 5
    positions2[i * 3 + 2] = (Math.random() - 0.5) * 10

    velocities2[i * 3] = (Math.random() - 0.5) * 0.02
    velocities2[i * 3 + 1] = Math.random() * 0.02 + 0.01
    velocities2[i * 3 + 2] = (Math.random() - 0.5) * 0.02
  }

  const geometry2 = new THREE.BufferGeometry()
  geometry2.setAttribute('position', new THREE.BufferAttribute(positions2, 3))

  const material2 = new THREE.PointsMaterial({
    color: 0xd3ad7f,
    size: 0.05,
    transparent: true,
    opacity: 0.6,
    blending: THREE.AdditiveBlending,
  })

  particles2 = new THREE.Points(geometry2, material2)
  scene.add(particles2)
  particles2.userData.velocities = velocities2

  const animate = () => {
    animationId = requestAnimationFrame(animate)

    if (particles1?.geometry?.attributes?.position) {
      const posAttr = particles1.geometry.attributes.position
      const positions = posAttr.array as Float32Array
      const velocities = particles1.userData.velocities as Float32Array
      for (let i = 0; i < particleCount; i++) {
        positions[i * 3] += velocities[i * 3]
        positions[i * 3 + 1] += velocities[i * 3 + 1]
        positions[i * 3 + 2] += velocities[i * 3 + 2]

        if (positions[i * 3 + 1] > 5) {
          positions[i * 3 + 1] = -5
          positions[i * 3] = (Math.random() - 0.5) * 15
          positions[i * 3 + 2] = (Math.random() - 0.5) * 10
        }
      }

      posAttr.needsUpdate = true
      particles1.rotation.y += 0.001
    }

    if (particles2?.geometry?.attributes?.position) {
      const posAttr = particles2.geometry.attributes.position
      const positions = posAttr.array as Float32Array
      const velocities = particles2.userData.velocities as Float32Array
      for (let i = 0; i < particleCount; i++) {
        positions[i * 3] += velocities[i * 3]
        positions[i * 3 + 1] += velocities[i * 3 + 1]
        positions[i * 3 + 2] += velocities[i * 3 + 2]

        if (positions[i * 3 + 1] > 5) {
          positions[i * 3 + 1] = -5
          positions[i * 3] = (Math.random() - 0.5) * 15
          positions[i * 3 + 2] = (Math.random() - 0.5) * 10
        }
      }

      posAttr.needsUpdate = true
      particles2.rotation.y += 0.001
    }

    if (renderer && scene && camera) {
      renderer.render(scene, camera)
    }
  }

  animate()
}

const initInfiniteScroll = () => {
  if (topScroll.value) {
    const scrollWidth = topScroll.value.scrollWidth / 2
    let position = 0

    const animateTop = () => {
      position -= 0.5
      if (Math.abs(position) >= scrollWidth) {
        position = 0
      }
      if (topScroll.value) {
        topScroll.value.style.transform = `translateX(${position}px)`
      }
      topAnimation = requestAnimationFrame(animateTop)
    }
    animateTop()
  }

  if (bottomScroll.value) {
    const scrollWidth = bottomScroll.value.scrollWidth / 2
    let position = -scrollWidth

    const animateBottom = () => {
      position += 0.5
      if (position >= 0) {
        position = -scrollWidth
      }
      if (bottomScroll.value) {
        bottomScroll.value.style.transform = `translateX(${position}px)`
      }
      bottomAnimation = requestAnimationFrame(animateBottom)
    }
    animateBottom()
  }
}

const handleResize = () => {
  if (!camera || !renderer) return

  camera.aspect = window.innerWidth / window.innerHeight
  camera.updateProjectionMatrix()
  renderer.setSize(window.innerWidth, window.innerHeight)
}

onMounted(() => {
  initParticles()
  initInfiniteScroll()

  if (logoRef.value) {
    gsap.from(logoRef.value, {
      opacity: 0,
      scale: 0.8,
      y: -50,
      duration: 1.5,
      ease: 'power3.out',
    })
  }

  if (creditsRef.value) {
    gsap.from(creditsRef.value.children, {
      opacity: 0,
      y: 30,
      duration: 1,
      stagger: 0.15,
      delay: 0.8,
      ease: 'power3.out',
    })
  }

  window.addEventListener('resize', handleResize)
})

onUnmounted(() => {
  if (topAnimation) cancelAnimationFrame(topAnimation)
  if (bottomAnimation) cancelAnimationFrame(bottomAnimation)
  if (animationId) cancelAnimationFrame(animationId)

  particles1?.geometry.dispose()
  ;(particles1?.material as THREE.Material)?.dispose()
  particles2?.geometry.dispose()
  ;(particles2?.material as THREE.Material)?.dispose()
  renderer?.dispose()

  window.removeEventListener('resize', handleResize)
})
</script>

<style scoped>
* {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
