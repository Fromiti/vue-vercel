<template>
    <div>

        <b-row>
            <b-col class="justify-content-center d-flex mb-4">
                <h1> PedidosEats - Node & Vue JS App </h1>
            </b-col>
        </b-row>

        <b-row class="d-flex justify-content-center">
            <template v-if="isUserLogged">
                <b-col cols="6" class="border">
                    <Meals/>
                </b-col>
                <b-col cols="5" class="border ml-5">
                    <Orders/>
                </b-col>
            </template>
            <template v-else>
                <b-nav>
                    <b-nav-item :to="{name:'Register'}"> Register </b-nav-item>
                    <b-nav-item :to="{name:'Login'}"> Login </b-nav-item>
                </b-nav>
                <b-container>
                    <router-view></router-view>
                </b-container>
            </template>
            <Carousel/>
        </b-row>
    </div>
</template>

<script>
    import Meals from "../components/pedidoseats/meals/Meals"
    import Orders from "../components/pedidoseats/orders/Orders"
    import Register from "../components/pedidoseats/auth/Register"
    import Login from "../components/pedidoseats/auth/Login"
    import Carousel from "../components/pedidoseats/Carousel";
    import {mapState, mapMutations} from 'vuex'

    export default {
        mounted() {
            const token = localStorage.getItem('token')
            const dataUser = JSON.parse(localStorage.getItem('userData'))
            if(token){
                this.changeUserState(true)
                this.userData = dataUser;
            }else{
                this.changeUserState(false)
            }
        },
        data() {
            return {
                userData: ''
            }
        },
        methods:{
            ...mapMutations(["changeUserState"]),
        },
        components:{
            Carousel,
            Meals,
            Orders,
            Register,
            Login
        },
        computed:{
            ...mapState(["isUserLogged"])
        }
    }
</script>