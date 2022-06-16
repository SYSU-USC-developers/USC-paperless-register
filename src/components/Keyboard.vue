<template>

	<div class="keyboard_box">
		<div v-for="row in keys">
			<SubKeyboard v-for="item in row" :curkey=item @click="ontouchkey(item)"></SubKeyboard>
		</div>
	</div>
</template>

<script setup lang="ts">
	import SubKeyboard from './SubKeyboard.vue'
	
	const enum Key {
		Key_0 = "0", Key_1 = "1", Key_2 = "2", Key_3 = "3", Key_4 = "4", Key_5 = "5", Key_6 = "6", Key_7 = "7", Key_8 =
			"8", Key_9 = "9", Key_del = "删除", Key_enter = "确定"
	};
	const keys: Key[][] = [
		[Key.Key_7, Key.Key_8, Key.Key_9],
		[Key.Key_4, Key.Key_5, Key.Key_6],
		[Key.Key_1, Key.Key_2, Key.Key_3],
		[Key.Key_del, Key.Key_0, Key.Key_enter]
	]
	import {
		ref,defineEmits
	} from 'vue';
	
	const em = defineEmits(['touchkey'])
	const ontouchkey = (e) => {
		em("touchkey", e)
	}
	

</script>

<style>
	.keyboard_box {
		background-color: #ffffff;
	}
</style>
