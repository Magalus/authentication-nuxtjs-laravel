<template>
    <div class="loginPage">
        <form @submit.prevent="login()">
            <input 
                type="email"
                v-model="form.email"
                placeholder="Email"
                ref="email"
                required
            >
            <input 
                type="password"
                v-model="form.password"
                placeholder="Mot de passe"
                required
            >
            <button type="submit">Se connecter</button>
            <div v-if="this.error" class="alert">{{ this.error }}</div>
            <a href="#">Mot de passe oublié ?</a>
            <NuxtLink to="/register">Créer nouveau compte</NuxtLink>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            form: {
                email: '',
                password: ''
            },
            error: undefined
        }
    },
    methods: {
        login() {
            this.$auth.loginWith('laravelSanctum', {
                data: this.form
            })
            .catch(error => {
               this.error = "Echec de connexion !"
            })
        },
    },
    mounted() {
        this.$refs.email.focus()
    }
}
</script>

<style lang="scss" scoped>

.loginPage {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;

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

    .alert {
        color: red;
        font-size: 14px;
        margin: 5px 0px;
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
}


</style>