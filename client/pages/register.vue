<template>
    <div class="registerPage">
        <form @submit.prevent="register()">
            <input 
                type="text"
                v-model="form.name"
                placeholder="Nom"
                ref="name"
                required
            >
            <div class="error">
                <span v-for="(name, index) in this.errors.name" :key="index">{{name}}</span>
            </div>
            <input 
                type="email"
                v-model="form.email"
                placeholder="Email"
                required
            >
            <div class="error">
                <span v-for="(email, index) in this.errors.email" :key="index">{{email}}</span>
            </div>
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
            <div class="error">
                <span v-for="(password, index) in this.errors.password" :key="index">{{password}}</span>
            </div>
            <button type="submit">S'inscrire</button>
            <NuxtLink to="/login">Déjà un compte ?</NuxtLink>
        </form>
    </div>
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
            errors: ''
        }
    },
    methods: {
        async register() {
            try {
                await this.$axios.get('/sanctum/csrf-cookie')
                await this.$axios.post('/api/register', this.form)
                await this.$auth.loginWith('laravelSanctum', {
                    data: {
                        email: this.form.email,
                        password: this.form.password
                    }
                })
                this.$router.push('/');
            } catch(e) {
                console.log(e.response.data.errors)
                this.errors = e.response.data.errors
            }
        }
    },
    mounted() {
        this.$refs.name.focus()
    }
}
</script>

<style lang="scss" scoped>

.registerPage {
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

    .error {
        display: inline-block;
        align-self: flex-start;
        color: red;
        font-size: 14px;
        margin-left: 10%;

        span {
            display: block;
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
}

</style>