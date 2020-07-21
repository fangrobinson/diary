<template>
    <v-container>
        <v-row
            align="center"
            justify="center"
        >
            <h1 class="display-2 font-weight-bold mb-3">
                {{ darkStatusMsg }}
            </h1>
        </v-row>
        <v-row
            align="center"
            justify="center"
        >
            <h1 class="display-2 font-weight-bold mb-3">
                {{ darkStatusMsg }}
            </h1>
        </v-row>
    </v-container>
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