<template>
    <div>
        <h1>{{ user.email }}</h1>
    </div>
</template>

<script>
export default {
    head() {
        return {
            title: `${this.user.first_name} ${this.user.last_name}`
        }
    },
    async asyncData({ params }) {
        const { id } = params;
        const res = await fetch(`https://reqres.in/api/users/${id}`)
        const data = await res.json()
        return {
            user: data.data
        }
    }
}
</script>

<style scoped>

</style>