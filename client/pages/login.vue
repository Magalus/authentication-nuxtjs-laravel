<template>
    <form @submit.prevent="login()">
        <input 
            type="email"
            v-model="form.email"
            placeholder="Email"
            required
        >
        <input 
            type="password"
            v-model="form.password"
            placeholder="Mot de passe"
            required
        >
        <button type="submit">Se connecter</button>
        <NuxtLink to="/forgot-password">Mot de passe oublié ?</NuxtLink>
        <NuxtLink to="/register">Créer nouveau compte</NuxtLink>
    </form>
</template>

<script>
export default {
    data() {
        return {
            form: {
                email: '',
                password: ''
            },
        }
    },
    methods: {
        async login() {
            try {
                await this.$auth.loginWith('laravelSanctum', {
                    data: this.form
                })
            } catch (e) {
                
            }
        },
    },
}
</script>

<style lang="scss" scoped>

form {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 400px;
    padding: 20px 0px;
    border-radius: 10px;
    border: 1px solid black;

    input {
        width: 80%;
        margin: 10px 0px;
        padding: 6px;
        border-width: 1px;
        border-radius: 5px;
    }

    button {
        width: 80%;
        margin: 10px 0px;
        padding: 6px;
        border-width: 1px;
        border-radius: 5px;

        &:hover {
            cursor: pointer;
            background-color: blue;
            color: white;
        }
    }
}

a {
    text-decoration: none;
    color: black;
    font-size: 14px;
    margin: 5px 0px;

    &:hover {
        color: blue;
    }
}


</style>