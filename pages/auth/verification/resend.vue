<template>
    <div>
        <Navigation />
        <div class="d-flex justify-content-center">
            <div class="card" style="width: 18rem;">
                <div class="card-body">
                    <h5 class="card-title">Resend</h5>
                    <form @submit.prevent="submit">
                        <div class="mb-3">
                            <label for="email" class="form-label">Email</label>
                            <input type="text" v-model="email" class="form-control" id="email">
                        </div>
                        <input type="submit" class="btn btn-primary" value="Resend">
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
                respond: {}
            };
    },
    methods: {
        submit() {
            const data = {
                "email": this.email
            }
            this.$axios.post('/verification/resend', data)
            .then(res => {
                console.log(res)
                this.respond = res
            })
            .catch(e => {
                console.log(e)
                this.respond = e
            })
        }
    }
}
</script>