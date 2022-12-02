<script setup lang="ts">
	import {ref} from "vue"
	import ValueInput from "@/components/ValueInput.vue"

	const emit = defineEmits(['submit', 'deleteEntry'])
	const submit = () => {
		emit('submit', { label: label.value, value: value.value })
		clearEntry()
	}
	const clearEntry = () => {
		label.value = ''
		value.value = 0
	}
	let label = ref('')
	let value = ref(0)
</script>

<template>
	<form @submit.prevent>
		<input type="text" v-model.trim="label" placeholder="Name of Price Component" />
		<ValueInput v-model:value="value" />
		<input type="submit" value="Submit" @click="submit" />
		<input type="button" id="delete" value="X" @click="clearEntry" />
	</form>
</template>

<style scoped>
form {
	display: flex;
}

input[type="text"] {
	flex: 1;
}
</style>
