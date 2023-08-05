<template>
  <VApp>
    <SideBar @changeColor="handleColorChange"/>
    <VMain>
      <ImageGallary :isWithColor="isWithColor"/>
    </VMain>
  </VApp>
</template>

<script setup>
  import SideBar from '@/components/SideBar.vue';
  import ImageGallary from '@/components/ImageGallary.vue';
  import {ref} from 'vue'

  const isWithColor = ref(true)
  const alert = ref(true)

  const handleColorChange = (isColorful) => {
    isWithColor.value = isColorful
  }

</script>
