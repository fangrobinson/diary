<template>
    <v-row v-if="entryData.body !== undefined">
        <v-col
            xs="12" offset-xs="0"
            sm="10" offset-sm="1"
            md="8" offset-md="2"
            lg="8" offset-lg="2"
            xl="4" offset-xl="4"
        >
            <v-card class="wrapper" flat>
                <h1> {{ entryData.place }} </h1>




                <h1>
                    {{ darkStatusMsg }} {{ entryData.place }}
                </h1>
            </v-card>

        </v-col>
    </v-row>
    <v-row v-else/>
</template>

<script>
export default {
    props: {
        filename: {
            type: String,
            default: ""
        },
    },

    name: "BlogEntry",

    data: () => ({
        entryData: {},
    }),

    computed: {
        darkStatusMsg() {
            return (this.$store.state.darkEnabled) ? 'Dark Mode: Enabled' : 'Dark Mode: Disabled'
        }
    },

    mounted () {
        import('../assets/entries/' + this.filename + ".json")
            .then(obj => this.entryData = obj)
    }
}
</script>

<style scoped>
    @import 'https://fonts.googleapis.com/css?family=Fira+Sans:300,300i,400,400i,500,500i,700,700i&subset=latin-ext';
    @import 'https://fonts.googleapis.com/css?family=Roboto+Mono:300,400&subset=latin-ext';
    @import 'https://cdnjs.cloudflare.com/ajax/libs/normalize/4.2.0/normalize.min.css';

    .wrapper {
        padding: 0 3vm 0 3vm;
    }
</style>