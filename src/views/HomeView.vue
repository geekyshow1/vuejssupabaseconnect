<script setup>
import { ref, onMounted } from 'vue'
import { supabase } from '../lib/supabaseClient';
const allproducts = ref([])

async function getProducts () {
  let { data: products, error } = await supabase.from('products').select('*')
  allproducts.value = products
}
onMounted(()=>{
  getProducts()
})
</script>

<template>
  <main>
   <ul>
    <li v-for="product in allproducts" :key="product.id">
      {{ product.title }} -- {{ product.price }}
    </li>
   </ul>
  </main>
</template>
