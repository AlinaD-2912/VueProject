<script setup lang="ts">
import { ref, computed } from 'vue';

const breads = [
    'Baguette',
    'Ciabatta',
    'Pain de seigle',
    'Wrap',
    'Pain aux céréales'
]
const sauces = [
    'Mayonnaise',
    'Moutarde',
    'Pesto',
    'Sauce barbecue',
    'Sauce aigre-douce'
]
const cheeses = [
    'Cheddar',
    'Mozzarella',
    'Gouda',
    'Emmental',
    'Roquefort'
]
const fillings = [
    'Jambon',
    'Poulet',
    'Saumon',
    'Thon',
    'Bacon'
]

const sandwich = ref({
    bread: "",
    sauce: "",
    cheese: "",
    filling: ""
})

const sandwichsList = ref<{ bread: string, sauce: string, cheese: string, filling: string }[]>([])

const generateSandwich = (): void => {
    sandwich.value.bread = breads[Math.floor(Math.random() * breads.length)]
    sandwich.value.sauce = sauces[Math.floor(Math.random() * sauces.length)]
    sandwich.value.cheese = cheeses[Math.floor(Math.random() * cheeses.length)]
    sandwich.value.filling = fillings[Math.floor(Math.random() * fillings.length)]
}

const addSandwich = (): void => {

    // prevents from adding empty sandwich
    if (!sandwich.value.bread) {
        alert("Can't add empty sandwich to the list")
        return
    }

    // some returns true or false if an identical sandwich already exists in the array
    const isDuplicate = sandwichsList.value.some(s =>
        s.bread === sandwich.value.bread &&
        s.sauce === sandwich.value.sauce &&
        s.cheese === sandwich.value.cheese &&
        s.filling === sandwich.value.filling
    )

    if (isDuplicate) {
        alert("Sandwich already exists in the list")
        return
    }

    // creates a copy of sandwich const to avoid pushing a reference
    sandwichsList.value.push({ ...sandwich.value })
}

const removeSandwich = (index: number): void => {
    sandwichsList.value.splice(index, 1)
}

const totalSandwichs = computed(() => sandwichsList.value.length)

const filterBread = ref<string>("")

const filteredList = computed(() => {
    // if nothing selected returns full list
    if (filterBread.value === "") {
        return sandwichsList.value
    }
    return sandwichsList.value.filter(s => s.bread === filterBread.value)
})

</script>

<template>

    <h1>Sandwich Generator</h1>

    <div>
        <button @click="generateSandwich" class="btn-generate">Générer un sandwich</button>

        <p v-if="!sandwich.bread">Sandwich is not yet generated</p>
        <p v-else>Generated sandwich with ingredients : Bread : {{ sandwich.bread }}, Sauce : {{ sandwich.sauce }},
            Cheese : {{sandwich.cheese }}, Filling : {{ sandwich.filling }}
        </p>
    </div>


    <button @click="addSandwich" class="btn-add">Sauvegarder</button>

    <ul>
        <!-- filter by bread -->
        <select v-model="filterBread" v-if="sandwichsList.length">
            <option value="">All</option>
            <option v-for="bread in breads" :key="bread" :value="bread">{{ bread }}</option>
        </select>

        <li v-for="(sandwich, index) in filteredList" :key="index">Sandwich {{ index + 1 }}: {{ sandwich.bread }}, {{
            sandwich.sauce }},
            {{ sandwich.cheese }}, {{ sandwich.filling }}
            <button @click="removeSandwich(index)" class="btn-delete">Supprimer</button>
        </li>
        <h2 v-if="sandwichsList.length">Total : {{ totalSandwichs }}</h2>
    </ul>


</template>

<style scoped>
.btn-generate {
    background-color: #2300b0;
    border: none;
    color: white;
    padding: 10px 10px;
    border-radius: 25px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
}

.btn-add {
    background-color: #006c10;
    border: none;
    color: white;
    padding: 5px 5px;
    border-radius: 25px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 14px;
    margin: 4px 2px;
    cursor: pointer;
}

.btn-delete {
    background-color: #b60000;
    border: none;
    color: white;
    padding: 5px 5px;
    border-radius: 25px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 14px;
    margin: 4px 2px;
    cursor: pointer;
}
</style>
