<script setup lang="ts">
import { computed } from 'vue'
import { RouterLink } from 'vue-router'

interface Props {
  variant?: 'primary' | 'secondary' | 'outline'
  size?: 'sm' | 'md' | 'lg'
  to?: string
  disabled?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  variant: 'primary',
  size: 'md',
  disabled: false,
})

const emit = defineEmits<{
  click: [event: MouseEvent]
}>()

const componentType = computed(() => {
  return props.to ? RouterLink : 'button'
})

const buttonClasses = computed(() => {
  const baseClasses =
    'inline-flex items-center justify-center font-semibold rounded-lg transition-all hover:scale-105 active:scale-95 transform disabled:opacity-50 disabled:cursor-not-allowed disabled:hover:scale-100 cursor-pointer'

  const sizeClasses = {
    sm: 'px-4 py-2 text-xs sm:px-5 sm:py-2 sm:text-sm',
    md: 'px-6 py-2.5 text-sm sm:px-8 sm:py-3 sm:text-base',
    lg: 'px-8 py-3 text-base sm:px-10 sm:py-4 sm:text-lg',
  }

  const variantClasses = {
    primary: 'bg-brew-tan text-brew-white hover:bg-brew-tan/90 shadow-md hover:shadow-lg',
    secondary: 'bg-white text-brew-dark hover:bg-brew-cream shadow-md hover:shadow-lg',
    outline:
      'bg-transparent border-2 border-brew-cream text-brew-cream hover:bg-brew-cream hover:text-brew-dark',
  }

  return `${baseClasses} ${sizeClasses[props.size]} ${variantClasses[props.variant]}`
})

const handleClick = (event: MouseEvent) => {
  if (!props.disabled) {
    emit('click', event)
  }
}
</script>

<template>
  <component
    :is="componentType"
    :to="to"
    :class="buttonClasses"
    :disabled="disabled"
    @click="handleClick"
  >
    <slot />
  </component>
</template>
