<script setup lang="ts">
import { ref } from "vue";

const emit = defineEmits(['submit', 'deleteEntry'])
const submit = () => {
	emit('submit', { label, value })
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
  <input type="text" v-model="label" placeholder="Name of Price Component" />
  <input type="number" v-model="value" placeholder="Value" />
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