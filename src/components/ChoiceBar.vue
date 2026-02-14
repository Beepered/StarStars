<template>
    <section class="bar">
        <p style="font-size: large; color: white;">Search</p>
        <p>Category: {{ category[0].toUpperCase() + category.slice(1) }}</p>
        <div class="grid">
            <button @click="SwitchCategory('films')">Film</button>
            <button @click="SwitchCategory('people')">People</button>
            <button @click="SwitchCategory('planets')">Planets</button>
            <button @click="SwitchCategory('starships')">Starships</button>
        </div>
        <div>
            <input type="number" v-model="num">
        </div>
        <button @click="FetchData(category)">Search</button>
    </section>
</template>

<script>
export default {
    data() {
        return {
            num: "1",
            category: "None"
        }
    },
    methods: {
        async FetchData(category) {
            try {
                const response = await fetch(`https://www.swapi.tech/api/${category}/${this.num}/`);
                // Check if the response was successful
                if (!response.ok) {
                    this.$emit('click-event', JSON.stringify("ERROR"));
                    throw new Error('Network response was not ok');
                }

                // Parse the response body to JSON
                const data = await response.json();

                // Get data's result
                this.$emit('click-event', JSON.stringify(data.result));

            } catch (error) {
                console.error('Error:', error);
            }
        },
        SwitchCategory(category) {
            this.category = category;
        }
    }
}
</script>

<style scoped>
.bar {
    background-color: rgb(177, 177, 177);
    border: 2px solid rgb(49, 49, 49);
    padding: 15px;
    text-align: center;
    min-width: 50%;
    max-width: 80%;
    min-height: 50%;
}

.grid {
    display: grid;
    grid-template-columns: auto auto auto;
    background-color: rgb(255, 254, 243);
    padding: 10px;
}

.grid button {
    background-color: #f1f1f1;
    border: 1px solid black;
    padding: 8px;
    font-size: 15px;
    text-align: center;
    border-radius: 5px;
}

.grid button:hover {
    background-color: #c7c7c7;
}

button {
    min-width: 25%;
    padding: 4px;
    margin: 5px;
}
</style>