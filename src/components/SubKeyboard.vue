<template>
	<button
	  type="button"
	>
	<a>{{curkey}}</a>
	</button>
</template>

<script setup lang="ts">
	
	import { reactive, ref } from 'vue';
	

	 
	type Props = {
	  curkey: Key
	}
	 
	defineProps<Props>()






</script>

<style>

	
	button{
		border-width: 0px;
		position: relative;
		width: 150px;
		height: 50px;
		margin: 20px;
		background-color: #00000000;
	}
	button a{
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		background: rgba(255,255,255,0.05);
		box-shadow: 0 15px 35px rgba(0,0,0,0.2);
		border-top: 1px solid rgba(255,255,255,0.1);
		border-bottom: 1px solid rgba(255,255,255,0.1);
		border-radius: 30px;
		color: #fff;
		z-index: 1;
		font-weight: 400;
		font-size: 1.6em;
		letter-spacing: 1px;/*字母间距*/
		text-decoration: none;
		overflow: hidden;
		transition: 0.5;
	}
	button:hover a{
		letter-spacing: 3px;
	}
	button a::before{
		content: "";
		position: absolute;
		top: 0;
		left: 0;
		width: 50%;
		height: 100%;
		background: linear-gradient(to left,rgba(255,255,255,0.15),transparent);
		transform:  skewX(45deg) translateX(0);
		transition: 0.5s;
	}
	button:hover a::before{
		transform:  skewX(45deg) translateX(200%);
	}

	
</style>