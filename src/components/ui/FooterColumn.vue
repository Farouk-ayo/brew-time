<script setup lang="ts">
interface FooterLink {
  name: string
  path: string
}

interface Props {
  title: string
  links: FooterLink[]
}

defineProps<Props>()
</script>

<template>
  <div class="sm:text-left">
    <h3 class="text-brew-tan font-semibold text-2xl md:text-3xl mb-4 sm:mb-5 tracking-wide">
      {{ title }}
    </h3>
    <ul class="space-y-2.5 sm:space-y-3">
      <li v-for="link in links" :key="link.path">
        <RouterLink
          :to="link.path"
          class="text-brew-cream/80 text-sm sm:text-base hover:text-brew-tan transition-colors duration-200 inline-block"
        >
          {{ link.name }}
        </RouterLink>
      </li>
    </ul>
  </div>
</template>
