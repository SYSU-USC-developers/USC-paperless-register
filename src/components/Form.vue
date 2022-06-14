<template>
    <el-form
        ref="elForm"
        class="form"
        label-width="100px"
        :model="formItem"
        size="large"
    >
        <el-form-item label="学工号">
            <el-input 
                v-model="formItem.idNumber"
                placeholder="请输入学工号"
            >
            </el-input>
        </el-form-item>

        <el-form-item label="手机号">
            <el-input 
                v-model="formItem.phoneNumber"
                placeholder="请输入手机号"
            >
            </el-input>
        </el-form-item>

        <el-form-item label="借伞数量">
            <el-input-number 
                v-model="formItem.umbrellaNumber"
                placeholder="1"
            >
            </el-input-number >
        </el-form-item>

        <el-form-item size="large">
            <el-button type="primary" @click="">提交</el-button>
            <el-button type="warning" @click="">重置</el-button>
        </el-form-item>
    </el-form>
    
</template>

<style>

.form {
    /* 设置位置 */
    margin: 0 auto;
    padding-top: 20px;
    padding-right: 20px;

    border: 3px solid #004E20;

    border-radius: 20px;

    /* 设置输入框的宽度 */
    max-width: 460px
}

</style>

<script setup lang="ts">

import { reactive } from 'vue'

const formItem = reactive({
  idNumber: '',
  phoneNumber: '',
  umbrellaNumber: 1
})

</script>