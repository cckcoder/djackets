<template>
    <div class="page-my-account">
        <div class="columns is-multiline">
            <div class="column is-12">
                <h1 class="title">My account</h1>
            </div>
            <div class="column is-12">
                <button @click="logOut()" class="button is-danger">Log out</button>
            </div>
            <hr>
            <div class="column is-12">
                <h2 class="subtitle">My orders</h2>
                <OrderSummary
                    v-for="order in orders"
                    :key="order.id"
                    :order="order"
                />
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import OrderSummary from '@/components/OrderSummary'

export default {
    name: 'MyAccount',
    data() {
        return {
            orders: []
        }
    },
    components: {
        OrderSummary
    },
    mounted() {
        document.title = 'My account | Djackets'
        this.getMyOrders()
    },
    methods: {
        logOut() {
            axios.defaults.headers.common["Authorization"] = ""

            localStorage.removeItem("token")
            localStorage.removeItem("username")
            localStorage.removeItem("userid")

            this.$store.commit('removeToken')
            this.$router.push('/')
        },
        async getMyOrders() {
            this.$store.commit('setIsLoading', true)

            await axios
                .get('/api/v1/orders/')
                .then(response => {
                    this.orders = response.data
                })
                .catch(error => {
                    console.log(error)
                })

            this.$store.commit('setIsLoading', false)
        }
    }
}
</script>

<style>

</style>
