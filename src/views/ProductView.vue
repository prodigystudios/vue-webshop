<template>
    <div class="main-wrapper">
        <img class="image" :src="'/pictures/' + image" width="350" height="350">
        <div class="container">
            <h1>{{ name }}</h1>
            <p class="wrap">{{ description }}</p>
        </div>
    </div>
    <p>Köp nu för {{ price }} kr</p>
    <router-link :to="'/cart/' + id"><button>KÖP</button></router-link>
</template>

<script>
export default {
    data() {
        return {
            id: 0,
            name: "",
            price: 0,
            description: "",
            image: null,
        }
    },
    created() {
        const id = this.$route.params.id
        fetch('http://localhost:5050/api/Products/' + id)
            .then(data => data.json())
            .then(products => {
                console.log(id)
                this.id = products.id,
                this.name = products.name,
                this.price = products.price,
                this.description = products.description
                this.image = products.image
            })
    }
}
</script>

<style scoped>
.main-wrapper {
    display: flex;
}

.image {
    margin-left: 100px;
}
.container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    margin-right: 390px;
}
.wrap {
    width: 50%;
    text-align: center;
}
 
button {
    background: transparent;
    border: none;
    border-radius: 5px;
    padding: 20px 40px;
    background-color: aquamarine;
    cursor: pointer;
}
button:hover {
    opacity: 0.75;
 }

</style>