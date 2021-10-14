<template>
    <div>
        <Navigation />
        <div class="d-flex justify-content-center">
            <div class="card" style="width: 18rem;">
                <div class="card-body">
                    <h5 class="card-title">Login</h5>
                    <form @submit.prevent="submit">
                        <div class="mb-3">
                            <label for="email" class="form-label">Email</label>
                            <input type="text" v-model="email" class="form-control" id="email">
                            <label for="password" class="form-label">Password</label>
                            <input type="password" v-model="password" class="form-control" id="password">
                        </div>
                        <input type="submit" class="btn btn-primary" value="Login">
                    </form>
                    {{ respond }}
                </div>
                <nuxt-link :to="{ name: 'verification.resend'}">Resend email verification</nuxt-link>
                <nuxt-link :to="{ name: 'password.email'}">Forgot you password?</nuxt-link>
            </div>
        </div>
    </div>
</template>

<script>
import Navigation from '@/components/Navigation.vue'

export default {
    components: {
        Navigation: Navigation
    },
    data() {
        return {
                email: '',
                password: '',
                respond: {}
            };
    },
    methods: {
        submit() {
            const user = {
                "email": this.email,
                "password": this.password
            }
            this.$auth.loginWith('local', { data: user})
            .then(res => {
                console.log(res),
                this.respond = res
            })
            .catch(err => {
                console.log(err),
                this.respond = err
            })
        }
    }
}
</script>