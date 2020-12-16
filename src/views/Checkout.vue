<template>
    <div class="checkout">
        <h1>{{title}}</h1>
        <CheckoutForm />
    </div>
</template>

<script>

    import CheckoutForm from "../components/CheckoutForm"
    export default {
        components: {
            CheckoutForm
        },
        data(){
            return {
                title: "Welcome to the checkout page"
            }
        }
    }
</script>

<style scoped>
    .checkout {
        width: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
</style>