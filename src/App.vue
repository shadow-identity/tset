<script setup lang="ts">
	import EditField from "@/components/EditField.vue"
	import ViewField from "@/components/ViewField.vue"
	import {reactive} from "vue"
	import type {PriceEntry, Prices} from "@/types"

	const state = reactive<Prices>(
		[
			{
				label: "Baseprice",
				value: 1,
				canDelete: false,
			},
			{
				label: "Scrap Surcharge",
				value: 10.101,
				canDelete: true,
			},
		],
	)

	const submit = ({ label, value }: PriceEntry) => {
		state.push({ label, value, canDelete: true })
	}
</script>

<template>
	<header>
		<h1>Price Components</h1>
	</header>
	<p class="total">Total: {{ state.reduce((total, priceEntry) => total + priceEntry.value, 0) }} EUR/kg</p>
	<section>
		<ul>
			<li v-for="(priceEntry) in state" :key="priceEntry.label">
				<ViewField
					v-model:value="priceEntry.value"
					:label="priceEntry.label"
					:canDelete="priceEntry.canDelete"
					@delete="state.splice(state.indexOf(priceEntry), 1)"
				/>
			</li>
			<EditField @submit="submit($event)" />
		</ul>
	</section>
</template>

<style scoped>
header {
	text-align: center;
}

.total {
	text-align: right;
}

li {
	list-style: none;
}
</style>
