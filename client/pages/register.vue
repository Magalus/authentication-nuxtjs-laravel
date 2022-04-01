<template>
    <form @submit.prevent="register()">
        <input 
            type="text"
            v-model="form.name"
            placeholder="Nom"
            required
        >
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
        <input 
            type="password"
            v-model="form.password_confirmation"
            placeholder="Confirmation du mot de passe"
            required
        >
        <button type="submit">S'inscrire</button>
        <NuxtLink to="/login">Déjà un compte ?</NuxtLink>
    </form>
</template>

<script>
export default {
    auth: false,
    data() {
        return {
            form: {
                name: '',
                email: '',
                password: '',
                password_confirmation: ''
            },
        }
    },
    methods: {
        async register() {
            try {
                await this.$axios.get('sanctum/csrf-cookie')
                await this.$axios.post('register', this.form)

                await this.$auth.loginWith('laravelSanctum', {
                    data: {
                        email: this.form.email,
                        password: this.form.password
                    }
                })
                this.$router.push('/');
            } catch(e) {
                
            }
        }
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