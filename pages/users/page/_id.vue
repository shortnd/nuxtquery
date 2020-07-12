<template>
  <div>
      <h1>All Users Page {{ users[0].id }}</h1>
      <ul>
          <li v-for="user in users" :key="user.id">
              <nuxt-link :to="`/users/${user.id}`">{{ user.email  }}</nuxt-link>
          </li>
      </ul>
      <hr>
      <ul>
          <li v-for="page in total_pages" :key="page">
              <nuxt-link :to="`/users/page/${page}`">{{ page }}</nuxt-link>
          </li>
      </ul>
  </div>
</template>

<script>
export default {
    async asyncData({ params }) {
        const res = await fetch(`https://reqres.in/api/users?page=${params.id}`);
        const data = await res.json();
        return {
            id: params.id,
            users: data.data,
            total_pages: data.total_pages
        }
    }
}
</script>

<style>

</style>