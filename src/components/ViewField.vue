<script setup lang="ts">
	import {ref} from 'vue'
	import ValueInput from "@/components/ValueInput.vue"

	const props = defineProps({
		label: String,
		value: Number,
		canDelete: Boolean,
	})
	const emit = defineEmits(['update:value', 'delete'])
	const submit = () => {
		emit('update:value', currentValue)
	}
	const deleteComponent = () => {
		emit('delete')
	}

	let currentValue = ref<number>(props.value ?? 0)
</script>

<template>
	<form @submit.prevent="submit">
		<label for="value">{{ label }}</label>
		<ValueInput v-model:value="currentValue" />
		<input type="submit" value="Submit" @click="submit" />
		<input
			type="button" id="delete" value="X" @click="deleteComponent"
			:style="{visibility: props.canDelete ? 'visible' : 'hidden'}"
		/>
	</form>
</template>


<style scoped>
form {
	display: flex;
}

label {
	flex: 1;
}
</style>
