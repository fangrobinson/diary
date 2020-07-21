<template>
    <v-menu
            v-model="value"
            :disabled="disabled"
            :absolute="absolute"
            :open-on-hover="openOnHover"
            :close-on-click="closeOnClick"
            :close-on-content-click="closeOnContentClick"
            :offset-y="offsetY"
    >
        <template v-slot:activator="{ on, attrs }">
            <v-app-bar-nav-icon
                    color="white"
                    dark
                    v-bind="attrs"
                    v-on="on"
            >
            </v-app-bar-nav-icon>
        </template>

        <v-list :class="darkMode">
            <v-list-item
                    v-for="(item, index) in items"
                    :key="index"
            >
                <v-list-item-title :class="darkMode">
                    <button @click="$store.commit('switchDark')">{{ darkModeButtonText }}</button>
                </v-list-item-title>
            </v-list-item>
        </v-list>
    </v-menu>
</template>

<script>
export default {
    data: () => ({
        items: [
            { title: '' },
        ],
        disabled: false,
        absolute: false,
        openOnHover: false,
        value: false,
        closeOnClick: true,
        closeOnContentClick: true,
        offsetX: false,
        offsetY: true,
    }),

    computed: {
        darkMode() {
            return (this.$store.state.darkEnabled) ? 'dark-mode' : 'light-mode'
        },
        darkModeButtonText() {
            return (this.$store.state.darkEnabled) ? 'Light Mode' : 'Dark Mode'
        }
    }
}
</script>
<style>
    .dark-mode {
        background-color: #3b3f42 !important;
        color: white !important;
    }
    .light-mode {
        background-color: white !important;
    }
</style>
