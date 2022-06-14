<template>
    <el-config-provider namespace="ep">
        <div class="main-content">
            <!-- sysu-log -->
            <div class="logo-area">
                <img alt="Vue logo" class="element-plus-logo" src="./assets/sysu-logo.png" />
            </div>
            <!-- entry -->
            <Entry class="entry" v-if="!isHidden" v-for="item in entryGroup" ref="refContent" :key="item.entryName"
                :entryName="item.entryName" :logoName="item.logoName" v-on:click="hideEntryShowForm">
            </Entry>
        </div>
    </el-config-provider>
</template>

<script lang="ts" setup>
// 导入一些包
import { ref } from 'vue'
// 用于渲染 Entry 中的文字和图片
const entryGroup = ref([
    {
        entryName: '雨伞借用',
        logoName: 'umbrella.png'
    },
    {
        entryName: '雨伞归还',
        logoName: 'umbrellaBack.png'
    },
    {
        entryName: '材料密封',
        logoName: 'letter.png'
    },
    {
        entryName: '丢卡领取',
        logoName: 'card.png'
    },
    {
        entryName: '车票改站',
        logoName: 'train.png'
    },
    {
        entryName: '补证领取',
        logoName: 'cardRenew.png'
    },
])
// 用于隐藏 Entry 的布尔变量
const isHidden = ref(false)

function hideEntryShowForm() {
    isHidden.value = true
}

</script>

<style>
#app {
    position: absolute;
    text-align: center;
    color: var(--ep-text-color-primary);
}

.main-content {
    text-align: center;
    vertical-align: middle;
}

.element-plus-logo {
    width: 50%;
}

.entry {
    margin-right: 100px;
    margin-bottom: 50px;
    margin-top: 50px;
}

.entry:nth-child(3n+1) {
    margin-right: 0;
}
</style>
