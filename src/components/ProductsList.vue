<template>
    <div class="products">
        <form class="searchbar">
            <input placeholder="поиск" v-model="search">
            <input type="submit"  class="btn">
        </form>
        <div class="product" v-for="(item) in filteredItems" v-bind:key="item.id">
            <div class="product-image">
                <img v-bind:src="item.src">
            </div>
            <div>
                <h4 class="product-title">
                    <router-link v-bind:to="'/product/' + item.id">
                        {{ item.item }}
                    </router-link>
                </h4>
                <label>{{item.price}}</label>
                <button class="btn" @click="addToCart(item.item,item.price)">Add to cart</button>  
            </div>
        </div>
    </div>
</template>
<script>
    import products from '../data/products.js'

    export default {
        data: function () {
            return {
                items: [],
                search: '',
                searchResult: [],
                cart: [],
                qwe: []
            };
        },
        mounted: function(){
            this.items = products;
                /*if (localStorage.getItem('cart')) {
                    try {
                    this.qwe = JSON.parse(localStorage.getItem('cart'));
                } catch(e) {
                    localStorage.removeItem('cart');
                }
            }*/
        },
        computed: {
            filteredItems: function() {
                console.log(this);
                if (!this.search) {
                    return this.items;
                }
                return this.items.filter(element => {
                    return element.item.toUpperCase().includes(this.search.toUpperCase());
                });
            },
        },
        methods:{
            addToCart: function(it, price){
                this.$store.commit('setCart', it);
                this.$store.commit('setP',price);
            },
            
        }
    }
</script>
