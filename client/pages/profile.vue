<template>
    <div class="ProfilePage">
        <form @submit.prevent="updateProfileInformation()">
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
            <button type="submit">Modifier</button>
        </form>
    </div>
</template>

<script>
export default {
    middleware: ['auth'],
    data() {
        return {
            form: {
                email: this.$auth.user.email,
                name: this.$auth.user.name
            },
        }
    },
    methods: {
        async updateProfileInformation() {
            try {
                await this.$axios.get('sanctum/csrf-cookie')
                await this.$axios.put('user/profile-information', this.form)

                await this.$auth.fetchUser()
            } catch (e) {

            }
        },
    },
}
</script>