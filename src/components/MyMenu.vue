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

        <v-list>
            <v-list-item
                    v-for="(item, index) in items"
                    :key="index"
            >
                <v-list-item-title>
                    {{ item.title }}
                    <button v-on:click="emitToParent">Dark Mode</button>
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

        methods: {
            emitToParent: function(){
                console.log("Te la creíste we ecsdi");
                console.log("Todavía me falta");
                console.log("Intenté pasar un emit a mi parent");
                console.log("Y actualizar los props del hijo");
                console.log("Probé bindear el prop con el return en data");
                console.log("Lo deje roto por ahora jejee despues sigo");
                this.$emit('trollear-jp');
            }
        },
    }
</script>
