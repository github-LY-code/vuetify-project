<template>
    <VNavigationDrawer expand-on-hover rail>
        <VList>
          <VListItem 
            prepend-avatar="https://randomuser.me/api/portraits/women/85.jpg" 
            title="Liu Yang"
            subtitle="2128803218@qq.com">
          </VListItem>
        </VList>

        <VDivider/>

        <VList density="compact" nav>
          <VListItem @click="changeColor(true)" prepend-icon="mdi-image" title="color"></VListItem>
          <VListItem @click="changeColor(false)" prepend-icon="mdi-dialpad" title="gray space"></VListItem>
        </VList>
    </VNavigationDrawer>
</template>

<script setup>
import {defineEmits} from 'vue'

const emits = defineEmits(['changeColor'])

const changeColor = (isColorful) => {
  emits("changeColor", isColorful)
}
</script>

<style setup>
.v-navigation-drawer {
  max-height: 100vh !important;
  position: fixed !important;
}
</style>