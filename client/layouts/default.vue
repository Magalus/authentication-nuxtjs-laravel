<template>
    <div>
        <Navbar/>
        <Nuxt/>
    </div>
</template>

<script>
import Navbar from "@/components/Navbar/navbar"

export default {
    components: {
        Navbar
    },
}
</script>

<style lang="scss">

body {
    margin: 0;
}

</style>