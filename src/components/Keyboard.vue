<template>
	<h1>{{NowInput}}</h1>
	<div class="keyboard_box">
		<div v-for="row in keys">
			<SubKeyboard v-for="item in row" :curkey=item @touchkey="ontouchkey"></SubKeyboard>
		</div>
	</div>
</template>

<script setup lang="ts">
	import SubKeyboard from './SubKeyboard.vue'
	const enum Key {Key_0 = "0", Key_1 = "1", Key_2 = "2", Key_3 = "3", Key_4 = "4", Key_5 = "5", Key_6 = "6", Key_7 = "7", Key_8 = "8", Key_9 = "9", Key_del = "→", Key_enter = "确定"};
	const keys:Key[][] = [[Key.Key_7,Key.Key_8,Key.Key_9],[Key.Key_4,Key.Key_5,Key.Key_6],[Key.Key_1,Key.Key_2,Key.Key_3],[Key.Key_del,Key.Key_0,Key.Key_enter]]
		import { reactive, ref } from 'vue';
	const NowInput : String = ref("111");
	const ontouchkey = (curkey:Key) => {
		// console.log(curkey)
		// if(curkey === Key.Key_del && NowInput.length > 0){
		// 	NowInput.slice(0,-1)
		// 	console.log(NowInput)
		// }else if(curkey === Key.Key_enter){
		// 	console.log(NowInput)
		// }else{
		// 	NowInput += curkey
		// 	console.log()
		// }
	}
	
	
</script>

<style>
	.keyboard_box{
		background-color: #333333;
	}
</style>