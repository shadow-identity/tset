<script setup lang="ts">
import EditField from "@/components/EditField.vue";
import ViewField from "@/components/ViewField.vue";
import { reactive } from "vue";
import type {Prices} from "@/types";

const state = reactive<Prices>([
		{
			label: "Baseprice",
			value: 1,
		},
		{
			label: "Scrap Surcharge",
			value: 10,
		},
	],
);
</script>

<template>
  <header>
    <h1>Price Components</h1>
  </header>
  <p class="total">Total: {{state.reduce((total, priceEntry) => total + priceEntry.value, 0) }} EUR/kg</p>
	<section>
		<ul>
			<li v-for="(priceEntry, index) in state" :key="index">
				<ViewField
						:label="priceEntry.label"
						:value="priceEntry.value"
						@newValue="priceEntry.value = $event"
						@delete="state.splice(index, 1)"
				/>
			</li>
			<EditField @submit="state.push($event)"/>
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
