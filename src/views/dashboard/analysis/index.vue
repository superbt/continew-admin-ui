<template>
  <div class="gi_page container">
    <a-space direction="vertical" :size="14" fill>
      <div> xbt 1
        <DataOverview />
      </div>
      <div> xbt2
        <a-grid :cols="24" :col-gap="14" :row-gap="14">
          <a-grid-item :span="{ xs: 24, sm: 24, md: 24, lg: 24, xl: 18, xxl: 18 }">
            xbt2_1
            <Geo />
          </a-grid-item>
          <a-grid-item :span="{ xs: 24, sm: 24, md: 24, lg: 24, xl: 6, xxl: 6 }">
            xbt2_2
            <Os style="margin-bottom: 16px" />
            <Browser />
          </a-grid-item>
        </a-grid>
      </div>
      <div> xbt3
        <a-grid :cols="24" :col-gap="16" :row-gap="16">
          <a-grid-item :span="{ xs: 24, sm: 24, md: 24, lg: 24, xl: 18, xxl: 18 }">
             xbt3_1
            <AccessTimeslot />
          </a-grid-item>
          <a-grid-item :span="{ xs: 24, sm: 24, md: 24, lg: 24, xl: 6, xxl: 6 }">
            xbt3_2
            <Module />
          </a-grid-item>
        </a-grid>
      </div>
    </a-space>
  </div>
</template>

<script setup lang="ts">
import DataOverview from './components/DataOverview/index.vue'
import Geo from './components/Geo.vue'
import Os from './components/Os.vue'
import Browser from './components/Browser.vue'
import Module from './components/Module.vue'
import AccessTimeslot from './components/AccessTimeslot.vue'

defineOptions({ name: 'Analysis' })
</script>

<style scoped lang="scss"></style>
