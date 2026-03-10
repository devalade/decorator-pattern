<script setup lang="ts">
import { ref, computed } from 'vue'

const hasMilk = ref(false)
const hasSugar = ref(false)
const hasWhip = ref(false)

const basePrice = 2.00
const total = computed(() => {
  let price = basePrice
  if (hasMilk.value) price += 0.50
  if (hasSugar.value) price += 0.30
  if (hasWhip.value) price += 0.80
  return price.toFixed(2)
})

const items = computed(() => {
  const list = ['☕ Café']
  if (hasMilk.value) list.push('🥛 Lait')
  if (hasSugar.value) list.push('🍬 Sucre')
  if (hasWhip.value) list.push('🍦 Chantilly')
  return list.join(' + ')
})
</script>

<template>
  <div class="demo">
    <div class="display">
      <div class="items">{{ items }}</div>
      <div class="price">{{ total }} €</div>
    </div>
    
    <div class="buttons">
      <button @click="hasMilk = !hasMilk" :class="{ on: hasMilk }">🥛 Lait</button>
      <button @click="hasSugar = !hasSugar" :class="{ on: hasSugar }">🍬 Sucre</button>
      <button @click="hasWhip = !hasWhip" :class="{ on: hasWhip }">🍦 Chantilly</button>
    </div>
  </div>
</template>

<style scoped>
.demo {
  background: #1e293b;
  padding: 1.5rem;
  border-radius: 8px;
  color: white;
}

.display {
  text-align: center;
  margin-bottom: 1rem;
}

.items {
  font-size: 1.2rem;
  margin-bottom: 0.5rem;
}

.price {
  font-size: 2rem;
  font-weight: bold;
  color: #fbbf24;
}

.buttons {
  display: flex;
  gap: 0.5rem;
  justify-content: center;
}

button {
  padding: 0.5rem 1rem;
  border: 1px solid #475569;
  background: #334155;
  color: white;
  border-radius: 4px;
  cursor: pointer;
}

button.on {
  background: #3b82f6;
  border-color: #3b82f6;
}
</style>
