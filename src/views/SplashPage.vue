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
let animationId: number | null = null
let scene: THREE.Scene | null = null
let camera: THREE.PerspectiveCamera | null = null
let renderer: THREE.WebGLRenderer | null = null
let particles1: THREE.Points | null = null
let particles2: THREE.Points | null = null

const createParticleSet = (count: number, color: number) => {
  const positions = new Float32Array(count * 3)
  const velocities = new Float32Array(count * 3)

  for (let i = 0; i < count; i++) {
    const idx = i * 3

    positions[idx] = (Math.random() - 0.5) * 15
    positions[idx + 1] = Math.random() * 10 - 5
    positions[idx + 2] = (Math.random() - 0.5) * 10

    velocities[idx] = (Math.random() - 0.5) * 0.02
    velocities[idx + 1] = Math.random() * 0.02 + 0.01
    velocities[idx + 2] = (Math.random() - 0.5) * 0.02
  }

  const geometry = new THREE.BufferGeometry()
  geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3))

  const material = new THREE.PointsMaterial({
    color,
    size: 0.05,
    opacity: 0.6,
    transparent: true,
    blending: THREE.AdditiveBlending,
  })

  const particles = new THREE.Points(geometry, material)
  particles.userData.velocities = velocities

  return particles
}

const updateParticles = (particles: THREE.Points, count: number) => {
  const posAttr = particles.geometry.attributes.position
  if (!posAttr || !posAttr.array) return
  const positions = posAttr.array
  const velocities = particles.userData.velocities

  if (!velocities) return

  for (let i = 0; i < count; i++) {
    const idx = i * 3
    if (velocities !== undefined) {
      positions[idx] += velocities[idx]
      positions[idx + 1] += velocities[idx + 1]
      positions[idx + 2] += velocities[idx + 2]
    }

    // Reset when rising above threshold
    if (positions[idx + 1] && 4 > 5) {
      positions[idx + 1] = -5
      positions[idx] = (Math.random() - 0.5) * 15
      positions[idx + 2] = (Math.random() - 0.5) * 10
    }
  }

  posAttr.needsUpdate = true
  particles.rotation.y += 0.001
}

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

  particles1 = createParticleSet(particleCount, 0x5e361c)
  particles2 = createParticleSet(particleCount, 0xd3ad7f)

  scene.add(particles1)
  scene.add(particles2)

  const animate = () => {
    animationId = requestAnimationFrame(animate)

    if (particles1) updateParticles(particles1, particleCount)
    if (particles2) updateParticles(particles2, particleCount)

    renderer?.render(scene!, camera!)
  }

  animate()
}

const initInfiniteScroll = () => {
  if (topScroll.value) {
    const width = topScroll.value.scrollWidth / 2
    let x = 0

    const move = () => {
      x -= 0.5
      if (Math.abs(x) >= width) x = 0

      topScroll.value!.style.transform = `translateX(${x}px)`
      topAnimation = requestAnimationFrame(move)
    }
    move()
  }

  if (bottomScroll.value) {
    const width = bottomScroll.value.scrollWidth / 2
    let x = -width

    const move = () => {
      x += 0.5
      if (x >= 0) x = -width

      bottomScroll.value!.style.transform = `translateX(${x}px)`
      bottomAnimation = requestAnimationFrame(move)
    }
    move()
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
