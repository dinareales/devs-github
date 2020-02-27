<template>
<div>
    <div>
        <UserHeader></UserHeader>
        <UserRepos></UserRepos>
    </div>
</div>
</template>

<script>
    import UserHeader from '@/components/Header.vue'
    import UserRepos from '@/components/Datatable.vue'

    export default {
        name: "UserDetails",
        components: {
            UserHeader,
            UserRepos
        },
        data() {
            return {
            }
        },
    }
</script>

<style scoped>

</style>
