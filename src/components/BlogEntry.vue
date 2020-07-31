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
                <h3 class="text-right"> {{ new Date(entryData.date) | date }} - {{ entryData.place }} </h3>

                <h1 v-if="entryData.title.length !== 0" class="text-center"> {{ entryData.title }} </h1>
                <p v-else></p>

                <div v-for="(elem, i) in entryData.body" :key="i" :class="[$vuetify.breakpoint.mdAndUp ? 'lg-font' : 'rg-font']">
                    <p
                        v-if="elem.type === 'text'"
                        class="entry-paragraph"
                    >
                        <span v-html="replaceNewLines(elem.content)"></span>
                    </p>

                    <br v-if="elem.type === 'empty'"/>

                    <ul v-if="elem.type === 'list'" class="ml-5">
                        <li
                            v-for="(item, i) in elem.items"
                            :key="i"
                        >{{ item }}</li>
                        <p></p>
                    </ul>

                    <ol v-if="elem.type === 'olist'" class="ml-5">
                        <li
                                v-for="(item, i) in elem.items"
                                :key="i"
                        >{{ item }}</li>
                        <p></p>
                    </ol>

                    <v-divider class="my-5 mx-8" v-if="elem.type === 'divider'" :dark="$store.state.darkEnabled"></v-divider>

                    <div v-if="elem.type === 'video' " align="center" :class="[videoContainerSize]">
                        <span v-html="videoSize(elem)"></span>
                    </div>

                    <br v-if="elem.type === 'place'"/>
                    <h5 v-if="elem.type === 'place'" :class="['text-right']"> {{ new Date(entryData.date) | date }} {{ elem.moment }} - {{ elem.name }} </h5>
                    <br v-if="elem.type === 'place'"/>

                    <v-carousel v-if="elem.type === 'carousel'" :height="carouselSize" :show-arrows="elem.items.length > 1" show-arrows-on-hover :hide-delimiters="elem.items.length === 1">
                        <v-carousel-item
                            class="hover-control"
                            v-for="(item,i) in elem.items"
                            :key="i"
                            :src="require('../assets/entries/img/' + item.src)"
                        >
                            <div class="img-title" v-if="item.title">{{ item.title }}</div>
                        </v-carousel-item>
                    </v-carousel>
                    <br v-if="elem.type === 'carousel'"/>
                </div>
            </v-card>

        </v-col>
    </v-row>
    <v-row v-else/>
</template>

<script>
import { createDateFilter } from "vue-date-fns";
import { es } from 'date-fns/locale';

export default {
    filters: {
        date: createDateFilter("dd MMMM yyyy - eeee ", { locale: es })
    },
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

        videoContainerSize() {
            return (this.$vuetify.breakpoint.mdAndUp) ? 'lg-video-container' : 'sm-video-container'
        },

        carouselSize() {
            return (this.$vuetify.breakpoint.mdAndUp) ? 600 : 200
        }
    },

    methods: {
        replaceNewLines(content) {
            content = content.replace(/\n/g, "</p><p>");
            return content;
        },
        videoSize(content) {
            return (this.$vuetify.breakpoint.mdAndUp) ? content.lgVideo : content.smVideo;
        },
        formatDate(aDate) {
            return this.$date(new Date(aDate), 'iiii MMMM yy', { locale: es } );
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
    .place-font {
        font-size: 100%;
    }
    .dark-mode {
        background-color: #2b2b2b !important;
        color: white !important;
    }
    .light-mode {
        background-color: white !important;
    }
    .lg-video-container {
    }

    .sm-video-container {
    }

    .img-title {
        display: none;
    }

    .hover-control:hover .img-title {
        display: flex;
        align-items: center;
        background: rgba(0,0,0,.3);
        height: 50px;
        justify-content: center;
        list-style-type: none;
        position: absolute;
        width: 100%;
        z-index: 1;
        color: whitesmoke;
    }

</style>