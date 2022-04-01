<template>
    <form @submit.prevent="resetPassword()">
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
        <button type="submit">Changer le mot de passe</button>
    </form>
</template>

<script>
export default {
    data() {
        return {
            form: {
                email: this.$route.query.email || '',
                password: '',
                password_confirmation: '',
                token: this.$route.query.token || ''
            },
        }
    },
    methods: {
        async resetPassword() {
            try {
                await this.$axios.get('sanctum/csrf-cookie')
                await this.$axios.post('reset-password', this.form)
                this.$router.push('/login')
            } catch (e) {
                
            }
        },
    },
}
</script>
