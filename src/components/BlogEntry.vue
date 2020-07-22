<template>
    <v-row v-if="entryData.body !== undefined">
        <v-col
            xs="12" offset-xs="0"
            sm="10" offset-sm="1"
            md="8" offset-md="2"
            lg="8" offset-lg="2"
            xl="8" offset-xl="2"
        >
            <v-divider class="my-5" :dark="$store.state.darkEnabled"></v-divider>
            <v-card :class="['wrapper pa-5', darkMode]" flat>
                <h3 class="text-right"> {{ entryData.date }} - {{ entryData.place }} </h3>

                <h1 v-if="entryData.title.length !== 0" class="text-center"> {{ entryData.title }} </h1>
                <p v-else></p>

                <div v-for="(elem, i) in entryData.body" :key="i" :class="[$vuetify.breakpoint.mdAndUp ? 'lg-font' : 'rg-font']">
                    <p
                        v-if="elem.type === 'text'"
                        class="entry-paragraph"
                    >
                        <span v-html="replaceNewLines(elem.content)"></span>
                    </p>

                    <v-img v-if="elem.type === 'img'" :src="require('../assets/entries/img/' + elem.path)"></v-img>

                    <ul v-if="elem.type === 'list'" class="ml-5">
                        <li
                            v-for="(item, i) in elem.items"
                            :key="i"
                        >{{ item }}</li>
                        <p></p>
                    </ul>

                    <v-divider class="my-5 mx-8" v-if="elem.type === 'divider'" :dark="$store.state.darkEnabled"></v-divider>

                    <div v-if="elem.type === 'video'" align="center" :class="[videoSize]">
                        <span v-html="elem.content"></span>
                    </div>

                </div>
            </v-card>

        </v-col>
    </v-row>
    <v-row v-else/>
</template>

<script>


export default {
    components: {
    },

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
        darkMode() {
            return (this.$store.state.darkEnabled) ? 'dark-mode' : 'light-mode'
        },

        videoSize() {
            return (this.$vuetify.breakpoint.mdAndUp) ? 'lg-video' : 'sm-video'
        }
    },

    methods: {
        replaceNewLines(content) {
            content = content.replace(/\n/g, "</p><p>");
            return content;
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
    .entry-paragraph {
        text-align: justify;
    }
    .lg-font {
        font-size: 145%;
    }
    .rg-font {
        font-size: 100%;
    }
    .dark-mode {
        background-color: #2b2b2b !important;
        color: white !important;
    }
    .light-mode {
        background-color: white !important;
    }
    .lg-video {
        top:0;
        left: 0;
        width: 100%;
        height: 100%;
    }
    .sm-video {
        top:0;
        left: 0;
        width: 40%;
        height: 40%;
    }
</style>