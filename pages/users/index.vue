<template>
    <div>
        <h1>Users</h1>
        <ul>
            <li v-for="user in users" :key="user.id">
                <nuxt-link :to="`/users/${user.id}`">{{ user.email }}</nuxt-link>
            </li>
        </ul>
        <ul>
            <li v-for="page in total_pages" :key="page">
                <nuxt-link :to="`/users?page=${page}`">{{ page }}</nuxt-link>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    head: {
        title: 'All Users'
    },
    watchQuery: ['page'],
    key: to => to.fullPath,
    async asyncData({ query }) {
        const page = parseInt(query.page) || 1;
        const res = await fetch(`https://reqres.in/api/users?page=${page}`);
        const data = await res.json();
        return {
            page,
            users: data.data,
            total_pages: data.total_pages
        }
    }
}
</script>