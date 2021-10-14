<template>
    <div>
        <Navigation />
        <div class="d-flex justify-content-center">
            <div class="card" style="width: 18rem;">
                <div class="card-body">
                    <h5 class="card-title">Reset password</h5>
                    <form @submit.prevent="submit">
                        <div class="mb-3">
                            <label for="email" class="form-label">Email</label>
                            <input type="text" readonly v-model="email" class="form-control" id="email">
                        </div>
                        <div class="mb-3">
                            <label for="password" class="form-label">Password</label>
                            <input type="password" v-model="password" class="form-control" id="password">
                        </div>
                        <div class="mb-3">
                            <label for="password_confirmation" class="form-label">Password confirmation</label>
                            <input type="password" v-model="password_confirmation" class="form-control" id="password_confirmation">
                        </div>
                        <input type="submit" class="btn btn-primary" value="Reset">
                    </form>
                    <p>{{ respond }}</p>
                </div>
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
                token: '',
                password: '',
                password_confirmation: '',
                respond: {}
            };
    },
    methods: {
        submit() {
            const data = {
                "email": this.email,
                "token": this.token,
                "password": this.password,
                "password_confirmation": this.password_confirmation
            }
            this.$axios.post('/password/reset', data)
            .then(res => {
                console.log(res),
                this.respond = res
            })
            .catch(err => {
                console.log(err),
                this.respond = err
            })
        }
    },
    created() {
        this.email = this.$route.query.email;
        this.token = this.$route.params.token;
    }
}
</script>
<style>
    
</style>