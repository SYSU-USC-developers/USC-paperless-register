<template>
  <el-config-provider namespace="ep">
    <div style="display: flex" class="main-content">
      <div>
        <img alt="Vue logo" class="element-plus-logo" src="./assets/sysu-logo.png" />
        <!-- <HelloWorld msg="Hello Vue 3.0 + Element Plus + Vite" /> -->
        <Entry entryName="借用雨伞"/>
      </div>
    </div>
  </el-config-provider>
</template>

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
