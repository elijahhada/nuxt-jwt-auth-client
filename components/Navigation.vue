<template>
    <nav class="navbar navbar-dark bg-dark">
        <span class="navbar-brand mb-0 h1">
            <nuxt-link :to="{ name: 'index'}" class="navbar-logo__text">Deadly app</nuxt-link>
        </span>
        <div class="ml-auto">
            <ul class="d-flex">
                <template v-if="!this.$auth.loggedIn">
                    <li>
                        <nuxt-link :to="{ name: 'login'}" class="navbar-link__text">Login</nuxt-link>
                    </li>
                    <li class="ml-5">
                        <nuxt-link :to="{ name: 'register'}" class="navbar-link__text">Register</nuxt-link>
                    </li>
                </template>
                <template v-else>
                    <li class="ml-5">
                        You are logged in as {{ this.$auth.user.name }}
                    </li>
                    <li class="ml-5" @click.prevent="logout">
                        Log out
                    </li>
                </template>
            </ul>
        </div>
    </nav>
</template>

<script>
export default {
    methods: {
        logout(){
            this.$auth.logout()
        }
    }
}
</script>

<style scoped>
    ul li {
        list-style: none;
        cursor: pointer;
        color: dodgerblue;
    }
    ul li:hover {
        color: rgb(30, 255, 30);
    }
    .navbar-logo__text, .navbar-link__text {
        color: dodgerblue;
    }
    .navbar-logo__text:hover, .navbar-link__text:hover {
        color: rgb(30, 255, 30);
    }
</style>
