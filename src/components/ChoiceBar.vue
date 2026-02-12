<template>
    <section class="bar">
        <p>Search</p>
        <button @click="FetchData('films')">Film</button>
        <button @click="FetchData('people')">People</button>
        <button @click="FetchData('planets')">Planets</button>
        <button @click="FetchData('starships')">Starships</button>
    </section>
</template>

<script>
export default {
    methods: {
        async FetchData(category) {
            try {
                const response = await fetch(`https://www.swapi.tech/api/${category}/1/`);
                // Check if the response was successful
                if (!response.ok) {
                    throw new Error('Network response was not ok');
                }

                // Parse the response body to JSON
                const data = await response.json();

                // Get data's result
                this.$emit('click-event', JSON.stringify(data.result));

            } catch (error) {
                console.error('Error:', error);
            }
        }
    }
}
</script>

<style scoped>
.bar {
    background-color: rgb(112, 112, 112);
    border: 2px solid black;
    padding: 15px;
    text-align: center;
    min-width: 50%;
    max-width: 80%;
}

button {
    min-width: 25%;
    min-height: 15%;
    margin: 5px;
}
</style>