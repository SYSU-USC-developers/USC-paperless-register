<template>
	<div class="form_div">
		<el-form ref="elForm" class="form" label-width="100px" :model="formItem" size="large">
		    <el-form-item label="学工号">
		        <el-input v-model="formItem.idNumber" placeholder="请输入学工号" @focus="oninputfocus('idNumber')" @blur="oninputblur">
		        </el-input>
		    </el-form-item>
		
		    <el-form-item label="手机号">
		        <el-input v-model="formItem.phoneNumber" placeholder="请输入手机号" @focus="oninputfocus('phoneNumber')" @blur="oninputblur">
		        </el-input>
		    </el-form-item>
		
		    <el-form-item label="借伞数量">
		        <el-input-number v-model="formItem.umbrellaNumber" placeholder="1" @focus="oninputfocus('umbrellaNumber')" @blur="oninputblur">
		        </el-input-number>
		    </el-form-item>
		
		    <el-form-item size="large">
		        <el-button type="primary" @click="postData">提交</el-button>
		        <el-button type="warning" @click="">重置</el-button>
		    </el-form-item>
		</el-form>
	</div>
	<div class="keyboard_div">
		<Keyboard @touchkey="ontouchkey"/>
	</div>
	

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
.form_div{
	width: 50%;
	display: inline-block;
}
.keyboard_div{
	width: 50%;
	display: inline-block;
}
</style>

<script setup lang="ts">

import { reactive,ref } from 'vue'
import axios from 'axios';
import Keyboard from './Keyboard.vue'

let curInput:String = ""


const formItem = reactive({
    idNumber: '',
    phoneNumber: '',
    umbrellaNumber: 1
})

const phoneNumberRef = ref(formItem.phoneNumber)

function postData() {
    axios.post('http://127.0.0.1:8256/register/umbrella/record', {
        firstName: 'Fred',
        lastName: 'Flintstone'
    })
        .then(function (response) {
            console.log(response);
        })
        .catch(function (error) {
            console.log(error);
        });
}

function oninputfocus(str:String){
	curInput = str
	
}

function oninputblur(){
	//curInput = ""
}

function ontouchkey(key){
	if(curInput === ""){
		return;
	}
	if(key === "确认"){
		
	}else if(key === ""){
		
	}else{
		formItem[curInput] += key
		console.log(key)
		console.log(curInput)
	}
}

</script>