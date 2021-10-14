<template>
    <div>
        <Navigation />
        <h3 v-if="success">{{ status }}</h3>
        <h3 v-else>{{ status }}</h3>
    </div>
</template>

<script>
import Navigation from '@/components/Navigation.vue'

export default {
    components: {
        Navigation: Navigation
    },
    async asyncData({ params, query, $axios }) {
        const q = await Object.keys(query)
        .map(k => `${k}=${query[k]}`)
        .join('&');

        try {
            const { data } = await $axios.post(
                `/verification/verify/${params.id}?${q}`
            );
            return { success: true, status: data.message };
        } catch(e) {
            console.log(e);
            return { success: false, status: e };
        }
    }
}
</script>