<template>
    <h1 class="display-2 font-weight-bold mb-3">
        {{ darkStatusMsg }}
    </h1>
</template>

<script>
export default {
    name: "BlogEntry",

    computed: {
        darkStatusMsg() {
            return (this.$store.state.darkEnabled) ? 'Dark Mode: Enabled' : 'Dark Mode: Disabled'
        }
    }
}
</script>

<style scoped>

</style>