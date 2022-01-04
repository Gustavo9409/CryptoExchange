<template>
  <div>
    <bounce-loader :loading="isLoading" :color="'#68d391'" :size="100" />
    <px-assets-table v-if="!isLoading" v-bind:assets="assets" />
  </div>
</template>

<script>
import PxAssetsTable from '@/components/PxAssetsTable.vue'
import api from '@/api'

export default {
  name: 'Home',
  components: { PxAssetsTable },
  data() {
    return {
      isLoading: false,
      isLoadingButt: false,
      assets: [],
    }
  },
  created() {
    this.isLoading = true
    this.isLoadingButt = true
   
    api.getAssets()
    .then((assets) => {
      this.assets = assets
    })
    .finally(() => {
      this.isLoading = false
      // this.$set(this.assets, 'isLoading', false)
    })
  },
}
</script>
