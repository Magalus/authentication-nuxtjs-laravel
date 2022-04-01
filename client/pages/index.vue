<template>
    <div>
        Welcome <span v-if="$auth.loggedIn">{{ this.$auth.user.name}}</span>
    </div>
</template>

<style lang="scss" scoped>

div {
    margin: auto;
    text-align: center;
    margin-top: 50px;
    font-size: 20px;
}

</style>


