<template>
    <div class="wrapper" v-if="isAuth">
        <app-navbar/>
        <app-sidebar/>

        <div class="content-wrapper">
            <router-view></router-view>
        </div>
        <app-footer/>
    </div>
    <div class="d-flex align-items-center justify-content-center vh-100 bg-light" v-else>
        <router-view></router-view>
    </div>
</template>

<script>
    import {mapState, mapGetters} from "vuex";
    import Footer from "./components/Footer.vue";
    import Navbar from "./components/Navbar.vue";
    import Sidebar from "./components/Sidebar.vue";

    export default {
        computed: {
            ...mapState(["token"]),
            ...mapGetters(["isAuth"])
        },
        components: {
            "app-footer": Footer,
            "app-navbar": Navbar,
            "app-sidebar": Sidebar
        }
    };
</script>
