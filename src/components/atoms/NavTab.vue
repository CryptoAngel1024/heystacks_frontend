<script lang="ts" setup>
interface Props {
  text: string
  selected?: boolean
}

defineProps<Props>()
</script>
<template>
  <div
    class="mx-2 min-w-[5rem] leading-10 hover:brightness-90 active:brightness-75 transition duration-200 cursor-pointer select-none flex-center"
    :class="selected && 'border-b-2 border-b-link text-link'"
  >
    {{ text }}
  </div>
</template>
