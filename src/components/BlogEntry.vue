<template>
    <v-row v-if="entryData.body !== undefined">
        <v-col
            xs="12" offset-xs="0"
            sm="10" offset-sm="1"
            md="8" offset-md="2"
            lg="8" offset-lg="2"
            xl="8" offset-xl="2"
        >
            <v-card class="wrapper" flat>
                <h3 class="text-right"> {{ entryData.date }} - {{ entryData.place }} </h3>

                <h1 v-if="entryData.title.length !== 0" class="text-center"> {{ entryData.title }} </h1>

                <div v-for="(elem, i) in entryData.body" :key="i">
                    <p v-if="elem.type==='text'">{{ elem.content }}</p>
                    <v-img v-if="elem.type==='img'" :src="require('../assets/entries/img/' + elem.path)"></v-img>
                </div>

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