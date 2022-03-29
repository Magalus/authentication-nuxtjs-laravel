<template>
    <nav v-if="$auth.loggedIn">
        <div class="navLinks">
            <NuxtLink to="/" class="link">Home</NuxtLink>
            <NuxtLink to="/contact" class="link">Contact</NuxtLink>
        </div>
        <div @click.prevent="logout()" class="link log">Déconnexion</div>
    </nav>
</template>

<script>
export default {
    methods: {
        async logout() {
            try {
                await this.$auth.logout()
            } catch (error) {
                console.log(error)
            }
        }
    }
}
</script>

<style lang="scss" scoped>

nav {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 50px;
    position: relative;
    background-color: black;

    .navLinks {
        display: flex;
    }

    .link {
        padding: 0px 10px;
        text-decoration: none;
        color: white;

        &:hover {
            cursor: pointer;
            color: #cc8e42;
        }
    }

    .log {
        position: absolute;
        right: 25px;
    }
}

</style>