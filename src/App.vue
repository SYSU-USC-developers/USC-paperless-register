<template>
    <el-config-provider namespace="ep">
        <div class="main-content">
            <!-- sysu-log -->
            <div class="logo-area">
                <img alt="Vue logo" class="element-plus-logo" src="./assets/sysu-logo.png" />
            </div>
            <!-- login -->
            <Login v-if="!hideLogin" @setFlagAndGiveID="setFlagAndReciveID"></Login>
            <!-- entry -->
            <Entry class="entry" v-if="!hideEntry" v-for="item in entryGroup" ref="refContent" :key="item.entryName"
                :entryName="item.entryName" :logoName="item.logoName" v-on:click="ShowForm">
            </Entry>
            <!-- form -->
            <UmbrellaForm v-if="!hideForm" :idNumerFromParent="idNumberRef" @emitSucceedSignal="receiveFlag"></UmbrellaForm>
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
// 一些变量
const idNumberRef = ref("")
// 用于隐藏和显示组件的布尔变量
const hideLogin = ref(false)
const hideEntry = ref(true)
const hideForm  = ref(true)
// 用于隐藏和显示组件的函数
function showLogin() {
    hideLogin.value = false
    hideEntry.value = true
    hideForm.value  = true
}
function ShowEntry() {
    hideLogin.value = true
    hideEntry.value = false
    hideForm.value  = true
}
function ShowForm() {
    hideLogin.value = true
    hideEntry.value = true
    hideForm.value  = false
}
// 接受登录返回的变量的函数
const setFlagAndReciveID = (isLoginFlag: boolean, idNumber: string) => {
    idNumberRef.value = idNumber

    console.log(idNumberRef.value)

    ShowEntry()
}
const receiveFlag = (succeedFlag: boolean) => {
    ShowEntry()
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
