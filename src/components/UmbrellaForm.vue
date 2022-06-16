<template>
    <el-form ref="elForm" class="form" label-width="100px" :model="formItem" size="large">
        <el-form-item label="学工号">
            <el-input v-model="formItem.idNumber" :value=idNumberRef :disabled="true">
            </el-input>
        </el-form-item>

        <el-form-item label="手机号">
            <el-input v-model="formItem.phoneNumber" placeholder="请输入手机号">
            </el-input>
        </el-form-item>

        <el-form-item label="是否代理">
            <el-radio-group v-model="formItem.proxy" v-on:change="handleProxyButton">
                <el-radio :label=true>是</el-radio>
                <el-radio :label=false>否</el-radio>
            </el-radio-group>
        </el-form-item>

        <el-form-item v-if="(formItem.proxy)" label="代理人学号">
            <el-input v-model="formItem.proxyIDNumber" placeholder="请输入代理人学号">
            </el-input>
        </el-form-item>

        <el-form-item label="借伞数量">
            <el-input-number v-model="formItem.umbrellaNumber" placeholder="1">
            </el-input-number>
        </el-form-item>

        <el-form-item size="large">
            <el-button type="primary" @click="postData">提交</el-button>
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
import axios from 'axios'
import { ref } from 'vue'

axios.defaults.withCredentials = true

// 通信变量
const props = defineProps({
    idNumerFromParent: String
})
const emit = defineEmits(['emitSucceedSignal'])

const tokenString = ref("")
const idNumberRef = ref(props.idNumerFromParent)
const succeedFlagRef = ref(false)

const formItem = reactive({
    idNumber: idNumberRef.value,
    proxyIDNumber: '',
    phoneNumber: '',
    umbrellaNumber: 1,
    proxy: false
})

function handleProxyButton(val: any) {
    console.log(formItem.proxy)
}

type getTokenRes = {
    timestamp: number;
    token: string
};

type GetTokenResponse = {
    data: getTokenRes
};

type CreateUserResponse = {
    sno: string,
    passwd: string
};

type UmbreallaPost = {
    phone: string;
    principal: string;
    proxy: boolean;
    quantity: number;
}

async function getToken() {
    try {
        const { data, status } = await axios.get<GetTokenResponse>(
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

async function getSession() {
    await getToken()

    try {
        const { data } = await axios.post<CreateUserResponse>(
            'http://127.0.0.1:8256/session',
            { 
                sno: '18327034', 
                passwd: '142313' 
            },
            {
                headers: {
                    Authorization: tokenString.value
                }
            },
        );
    } catch (error) {
        if (axios.isAxiosError(error)) {
            console.log('error message: ', error.message);
            // 👇️ error: AxiosError<any, any>
            return error.message;
        } else {
            console.log('unexpected error: ', error);
            return 'An unexpected error occurred';
        }
    }
}

async function postData() {
    await getSession()

    try {
        const { data, status } = await axios.post<UmbreallaPost>(
            'http://127.0.0.1:8256/register/umbrella/record',
            {
                phone: formItem.phoneNumber,
                proxy: formItem.proxy,
                principal: formItem.proxyIDNumber,
                quantity: formItem.umbrellaNumber
            },
            {
                headers: {
                    Authorization: tokenString.value,
                },
            },
        );

        succeedFlagRef.value = true
        emitSucceedSignal()
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

const emitSucceedSignal = () => {
    const succeedFlag = succeedFlagRef.value
    emit("emitSucceedSignal", succeedFlag)
}

</script>