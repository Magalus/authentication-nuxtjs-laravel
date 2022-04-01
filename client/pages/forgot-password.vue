<template>
    <form @submit.prevent="sendForgotPasswordEmail()">
        <input 
            type="email"
            v-model="form.email"
            placeholder="Email"
            required
        >
        <button type="submit">Réinitialiser le mot de passe</button>
    </form>
</template>

<script>
export default {
    data() {
        return {
            form: {
                email: '',
            },
        }
    },
    methods: {
        async sendForgotPasswordEmail() {
            try {
                await this.$axios.get('sanctum/csrf-cookie')
                await this.$axios.post('forgot-password', this.form)
            } catch (e) {
                
            }
        },
    },
}
</script>