<template>
  <VCard class="mx-5 my-2 pa-3">
    <VRow>
      <VExpandTransition>
        <VCard @vnode-mounted="autoclose" v-if="copyDialogVisiable" class="notify">
            <VAlert  
              text="你已成功复制此图片的地址！" 
              type="success" 
              variant="tonal"
            />
        </VCard>
      </VExpandTransition>

      <template v-for="(image, index) in imageLayout" :key="index">
        <VCol :cols="image.cols">
          <VHover v-slot="{ isHovering, props }" close-delay="200">
            <VCard 
              :elevation="isHovering ? 16 : 2" 
              :class="{ 'on-hover': isHovering }" 
              class="mx-auto" 
              v-bind="props"
              @click='copyUrl(`https://picsum.photos/500/300?image=${index * 5 + 10}${p.isWithColor ? "" : "&grayscale"}`)'
            >
              <VImg 
                :src='`https://picsum.photos/500/300?image=${index * 5 + 10}${p.isWithColor ? "" : "&grayscale"}`'
                :lazy-src='`https://picsum.photos/500/300?image=${index * 5 + 10}${p.isWithColor ? "" : "&grayscale"}`'
                aspect-ratio="1" 
                cover 
                class="bg-grey-lighten-2"
              >
                <template v-slot:placeholder>
                  <VRow 
                    class="fill-height ma-0" 
                    align="center" 
                    justify="center"
                  >
                    <VProgressCircular indeterminate color="grey-lighten-5"/>
                  </VRow>
                </template>
              </VImg>
            </VCard>
          </VHover>
        </VCol>
      </template>
    </VRow>
  </VCard>
</template>

<script setup>
import { defineProps,ref } from 'vue'

const p = defineProps(['isWithColor'])

const imageCount = 200
const cols = 1
const imageLayout = []
const copyDialogVisiable = ref(false)

for (let i = 0; i < imageCount; i++) {
  imageLayout.push({ cols: cols })
}

const copyUrl = async (url) => {
  await navigator.clipboard.writeText(url)
  // alert('你已成功复制此图片的地址')
  copyDialogVisiable.value = true
}

const autoclose = ()=> {
  setTimeout(()=> {
    copyDialogVisiable.value = false
  }, 1000)
}
</script>

<style scoped>
.notify {
  position: fixed;
  z-index: 1;
  left: 50%;
  transform: translateX(-50%);
}
</style>