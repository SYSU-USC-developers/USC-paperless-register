<template>
  <el-config-provider namespace="ep">
    <div style="display: flex" class="main-content">
      <div>
        <img alt="Vue logo" class="element-plus-logo" src="./assets/sysu-logo.png" />
        <Entry entryName="雨伞借用"/>
      </div>
    </div>
  </el-config-provider>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
const entryGroup = ref([
  {
    entryName: '雨伞借用',
    logoName: 'umbrella.png'
  },
  {
    entryName: '雨伞归还',
    logoName: 'umbrella.png'
  },
  {
    entryName: '材料密封',
    logoName: 'umbrella.png'
  },
  {
    entryName: '校卡领取',
    logoName: 'umbrella.png'
  },
  {
    entryName: '车票改站',
    logoName: 'umbrella.png'
  },
  {
    entryName: '补证领取',
    logoName: 'umbrella.png'
  },
])
</script>

<style>
#app {
  position: absolute;
  text-align: center;
  color: var(--ep-text-color-primary);
}

.element-plus-logo {
  width: 50%;
}
</style>
