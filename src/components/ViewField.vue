<script setup lang="ts">
import { ref } from 'vue';
const props = defineProps({
	label: String,
	value: Number,
})
const emit = defineEmits(['newValue', 'delete'])
const submit = () => {
	emit('newValue', currentValue)
}
const deleteComponent = () => {
	emit('delete')
}

let currentValue = ref<number>(props.value ?? 0)

</script>

<template>
  <form @submit.prevent="submit">
    <label for="value">{{ label }}</label>

    <input type="number" id="value" v-model="currentValue" @input="submit"/>
		<input type="submit" value="Submit" @click="submit" />

    <input type="button" id="delete" value="X" @click="deleteComponent" />

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