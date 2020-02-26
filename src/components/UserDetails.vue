<template>
<div>
    <div>
        <UserHeader></UserHeader>
    </div>
</div>
</template>

<script>
    import UserHeader from '@/components/Header.vue'

    export default {
        name: "UserDetails",
        components: {
            UserHeader
        },
        data() {
            return {
            }
        },
    }
</script>

<style scoped>

</style>
