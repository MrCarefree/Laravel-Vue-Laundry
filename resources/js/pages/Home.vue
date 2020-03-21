<template>
    <app-header title="Dashboard" :breadcumb="{parent: ['Home'], active: 'Starter Page'}"></app-header>
</template>
<script>
    import Header from "../components/Header";
    export default {
        components: {
            "app-header": Header
        }
    };
</script>
