<template>
	<view>
		<view class="p-4 bg-white">
			<up-box height="160px" gap="12px" :bgColors="['#EEFCFF', '#FCF8FF', '#FDF8F2']">
				<template #left>
					左
				</template>
				<template #rightTop>
					右上
				</template>
				<template #rightBottom>
					右下
				</template>
			</up-box>
		</view>

		<view>
			<up-list class="up-p-10">
				<up-list-item v-for="(item, index) in indexList" :key="index">
					<up-cell :title="item.title" @click="item.onclick">
						<!-- 	<template #icon>
							<up-avatar shape="square" size="35" :src="item.url"
								customStyle="margin: -3px 5px -3px 0"></up-avatar>
						</template> -->
					</up-cell>
				</up-list-item>
			</up-list>
		</view>
	</view>
</template>

<script setup>
	import { ref } from 'vue'

	const handleClick = () => {
		console.log(11);
	}
	const indexList = [{
		title: '设置',
		onclick: handleClick
	}]
</script>

<style>

</style>