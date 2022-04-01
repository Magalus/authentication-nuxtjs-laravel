<template>
    <nav>
        <div class="navLinks">
            <NuxtLink to="/" class="link">Home</NuxtLink>
            <NuxtLink to="/contact" class="link">Contact</NuxtLink>
            
        </div>

        <div class="logs">
            <div v-if="!$auth.loggedIn">
                <NuxtLink to="/login" class="link">Se connecter</NuxtLink>
                <NuxtLink to="/register" class="link">S'enregistrer</NuxtLink>
            </div>
            <div v-else>
                <NuxtLink to="/profile" class="link">{{this.$auth.user.name}}</NuxtLink>
                <span @click.prevent="logout()" class="link">Déconnexion</span>
            </div>
        </div>

        
    </nav>
</template>

<script>
export default {
    methods: {
        async logout() {
            await this.$auth.logout()
            this.$router.push('/')
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

    .logs {
        position: absolute;
        right: 25px;
    }
}

</style>