<script setup lang="ts">
	import {ref} from "vue";

	const props = defineProps({ value: Number })
	const emit = defineEmits(['update:value'])

	const makePretty = (value: number) => {
		const rowFractionStr = value.toString().split('.')[1] ?? '0'
		let [whole, fraction] = [Math.floor(value), Math.round(value % 1 * 100)]
		return `${whole}.${rowFractionStr.length > 2 ? fraction : rowFractionStr}`
	}

	let rawValue = ref<number>(props.value ?? 0)
	const prettyValue = ref<string>(makePretty(rawValue.value))

	const isActive = ref(false)
	const switchActive = () => {
		isActive.value = !isActive.value
	}

	const updateNumber = (inputValue: string) => {
		const value = parseFloat(inputValue) || 0
		rawValue.value = value
		prettyValue.value = makePretty(value)
	}

	const submitNumber = () => {
		emit('update:value', rawValue.value)
		switchActive()
	}
</script>

<template>
	<input
			type="text"
			:value="isActive ? rawValue : prettyValue"
			@input="updateNumber($event.target.value)"
			@focus="switchActive"
			@blur="submitNumber"
			pattern="[0-9]*(.([0-9])*)?"
	/>
</template>

<style scoped>
input {
	max-width: 4rem;
}

input:invalid {
	background-color: PeachPuff;
}
</style>
