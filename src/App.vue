<script setup>
import TheHeader from "@/components/TheHeader.vue";
import ProductCard from "@/components/ProductCard.vue";
import { useProductStore } from "./stores/productStore";
import { storeToRefs } from "pinia";
import { useCartStore } from "./stores/CartStore";
const productStore = useProductStore();
const cartStore = useCartStore();
const { products } = storeToRefs(useProductStore());
productStore.fill();

const addItems = (count, product) => {
	count = parseInt(count);
	cartStore.$patch(state => {
		for (let index = 0; index < count; index++) {
			state.items.push(product);
		}
	})
};
</script>

<template>
	<div class="container">
		<TheHeader />
		<ul class="sm:flex flex-wrap lg:flex-nowrap gap-5">
			<ProductCard v-for="product in productStore.products" :key="product.name" :product="product"
				@addToCart="cartStore.addItems($event, product)" />
		</ul>
	</div>
</template>