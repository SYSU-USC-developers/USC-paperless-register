<template>
    <el-form ref="elForm" class="form" label-width="100px" :model="formItem" size="large">
        <el-form-item label="学工号">
            <el-input v-model="formItem.idNumber" placeholder="请输入学工号" v-on:input="changeIDNumberRef">
            </el-input>
        </el-form-item>

        <el-form-item label="查询密码">
            <el-input v-model="formItem.password" placeholder="请输入查询密码" v-on:input="changePasswordRef">
            </el-input>
        </el-form-item>

        <el-form-item size="large">
            <el-button type="primary" @click="readInputAndPost">提交</el-button>
            <el-button type="warning" @click="">读卡</el-button>
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

<script lang="ts" setup>
// 导入的包
import { reactive } from 'vue'
import { ref } from 'vue'
import axios from 'axios'

// 表格结构
const formItem = reactive({
    idNumber: '',
    password: ''
})

// 一些变量
const isLogin = ref(false)
const idNumberRef = ref('')
const passwordRef = ref('')
const tokenString = ref('')
const emit = defineEmits(['setFlagAndGiveID'])  // 用于向父组件传送信息

// 结构体
// 接受 token 的结构体
type getTokenRes = {
    exp: number
    token: string
};
type GetTokenResponse = {
    data: getTokenRes
};
// 提交信息登录的结构体
type CreateUserResponse = {
    sno: string,
    passwd: string
};

// 函数
// input 监听函数
function changeIDNumberRef(inputString: string) {
    idNumberRef.value = inputString
}
function changePasswordRef(inputString: string) {
    passwordRef.value = inputString
}
// 获取 token 的函数
async function getToken() {
    try {
        const { data } = await axios.get<GetTokenResponse>(
            'http://127.0.0.1:8256/jwt/device'
        );

        tokenString.value = data.data.token
    } catch (error) {
        if (axios.isAxiosError(error)) {
            console.log('error message: ', error.message);
            return error.message;
        } else {
            console.log('unexpected error: ', error);
            return 'An unexpected error occurred';
        }
    }
}
// 提交按钮的函数
async function readInputAndPost() {
    await getToken()

    try {
        const { data, status } = await axios.post<CreateUserResponse>(
            'http://127.0.0.1:8256/session',
            {
                sno: idNumberRef.value,
                passwd: passwordRef.value
            },
            {
                headers:
                {
                    Authorization: tokenString.value
                }
            }
        )

        isLogin.value = true
        setFlagAndGiveID()

    } catch (error) {
        if (axios.isAxiosError(error)) {
            console.log('error message: ', error.message);
            return error.message;
        } else {
            console.log('unexpected error: ', error);
            return 'An unexpected error occurred';
        }
    }
}

// 提交信息给父组件
const setFlagAndGiveID = () => {
    const isLoginFlag = isLogin.value
    const idNumber    = idNumberRef.value
    emit("setFlagAndGiveID", isLoginFlag, idNumber)
}

</script>