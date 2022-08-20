<template>
    <div class="wrapper-shop" v-for="p in products" :key="p.id">
        <div class="container">
            <router-link :to="'/products/' + p.id"><img :src="'/pictures/' + p.image" width="350" height="350"></router-link>
            <h2>{{ p.name }}</h2>
            <p>{{ p.price }} kr</p>
        </div>
    </div>
</template>
<script>

export default {
    name: 'Product List',
    data() {
        return {
            imageLink: '',
            products: []
        }
    },
    created() {
        fetch('http://localhost:5050/api/Products')
            .then(response => response.json())
            .then(products => {
                this.products = products
            })
    },

}
</script>

<style scoped> 
.wrapper-shop {
    display: flex;
    position: relative;
    flex-wrap:wrap;
    float:left;
    left: 12.3rem;
    margin-left: 5px;
}
.container {
    border-radius: 7px;
    border: 1px solid;
    padding: 10px 10px;
}
</style>