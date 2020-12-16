<template>
    <form class="checkout-form" v-on:submit.prevent="onSubmit">
        <div class="form-group">
            <label for="name">Name:</label>
            <input type="text" id="name" name="name" v-model="name">
        </div>
        <div class="form-group">
            <label for="email">Email:</label>
            <input type="email" id="email" name="email" v-model="email">
        </div>
        <div class="form-group">
            <label for="address">Delivery Address:</label>
            <input type="text" id="address" name="address" v-model="address">
        </div>
        <div class="form-group">
            <ul class="items">
                <li v-for="(product, index) in products" :key="index">{{product.item}} | {{product.price}} | {{product.description}}</li>
            </ul>
        </div>
        <button class="submit-btn">Submit</button>
    </form>
</template>

<script>
    import axios from "axios"

    export default {
        data(){
            return {
                name: null,
                email: null,
                address: null,
                products: {}
            }
        },
        created(){
            axios.get("http://localhost:3000/products")
            .then(response => {
                this.products = response.data
                console.log(this.products)
            })
            .catch(error => {
                console.log(error.response)
            })
        },
        methods: {
            onSubmit(){
                let checkoutItems = {
                    name: this.name,
                    email: this.email,
                    address: this.address
                }

                axios.post(`http://localhost:3000/submit`, {
                    body: checkoutItems
                });

                console.log(checkoutItems)

                return checkoutItems
            }
        }
    }
</script>

<style scoped>
    .checkout-form {
        padding: 50px;
        box-shadow: 0 1px 1px 1px rgba(0, 0, 0, .4);
        border-radius: 5px;
    }

    .form-group {
        display: flex;
        flex-direction: column;
        margin: 25px 0;
    }

    input {
        padding: 10px;
        margin-top: 15px;
        border: none;
        box-shadow: 0 .5px .5px .5px rgba(0, 0, 0, 4);
        border-radius: 5px;
    }

    .submit-btn {
        width: 100%;
        padding: 10px;
        color: #fff;
        border: none;
        border-radius: 5px;
        background-color: rgb(0, 140, 255);
    }

    .submit-btn:hover {
        background-color: rgb(1, 104, 189);
        cursor: pointer;
    }
</style>