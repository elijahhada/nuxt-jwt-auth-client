<template>
    <div>
        <Navigation />
        <div class="d-flex justify-content-center">
            <div class="card" style="width: 18rem;">
                <div class="card-body">
                    <h5 class="card-title">Register</h5>
                    <form @submit.prevent="submit">
                        <div class="mb-3">
                            <label for="fullname" class="form-label">Full name</label>
                            <input type="text" v-model="username" class="form-control" id="fullname">
                            <label for="name" class="form-label">User name</label>
                            <input type="text" v-model="name" class="form-control" id="name">
                            <label for="email" class="form-label">Email</label>
                            <input type="text" v-model="email" class="form-control" id="email">
                            <label for="password" class="form-label">Password</label>
                            <input type="password" v-model="password" class="form-control" id="password">
                            <label for="password_confirmation" class="form-label">Password confirmation</label>
                            <input type="password" v-model="password_confirmation" class="form-control" id="password_confirmation">
                        </div>
                        <input type="submit" class="btn btn-primary" value="Register">
                    </form>
                    <p v-if="isOk">You have to confirm your email now</p>
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
                username: '',
                name: '',
                email: '',
                password: '',
                password_confirmation: '',
                respond: {},
                isOk: false
            };
    },
    methods: {
        submit(){
            const user = {
                "username": this.username,
                "name": this.name,
                "email": this.email,
                "password": this.password,
                "password_confirmation": this.password_confirmation,
            }
            this.$axios.post('/register', user)
            .then(
                res => {
                    console.log(res)
                    this.respond = res.data
                    if(res.status === 200){
                        this.isOk = true,
                        this.username = '',
                        this.name = '',
                        this.email = '',
                        this.password = '',
                        this.password_confirmation = ''
                    }
                }
            )
            .catch(
                err => console.log(err)
            )
        }
    }
}
</script>
