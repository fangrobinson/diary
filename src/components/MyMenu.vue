<template>
    <v-row align="center">
        <v-menu
                v-model="value"
                :disabled="disabled"
                :absolute="absolute"
                :open-on-hover="openOnHover"
                :close-on-click="closeOnClick"
                :close-on-content-click="closeOnContentClick"
                :offset-x="offsetX"
                :offset-y="offsetY"
        >
            <template v-slot:activator="{ on, attrs }">
                <v-btn
                        color="primary"
                        dark
                        v-bind="attrs"
                        v-on="on"
                >
                    Dropdown
                </v-btn>
            </template>
            <v-list>
                <v-list-item
                        v-for="(item, index) in items"
                        :key="index"
                >
                    <v-list-item-title>{{ item.title }}</v-list-item-title>
                </v-list-item>
            </v-list>
        </v-menu>
    </v-row>
</template>

<script>
    export default {
        data: () => ({
            items: [
                { title: 'Click Me' },
                { title: 'Click Me' },
                { title: 'Click Me' },
                { title: 'Click Me 2' },
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
    }
</script>
