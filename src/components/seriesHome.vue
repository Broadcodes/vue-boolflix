<template>
    <div class="bg-page">
        <!-- Pagina dedicata solo alle serie accedendo dalla homepage cliccando in series nell'header -->
        <div class="titleSeries">
            <div id="jumbo">
                <img src="@/assets/img/seriesPoster.png" alt="seriesPoster">
                <h2 id="jumboText">Ore e ore di intrattenimento con le migliori serie. Un esclusiva solo di Boolflix
                </h2>
            </div>
            <span>
                <h1>Tutte le serie disponibili su</h1>
                <img id="logo" src="@/assets/img/boolflix_logo.png" alt="boolflix logo">
            </span>
        </div>
        <!-- permette di visualizzare più dati in base alla lettera dell'alfabeto presente nella pagina -->
        <SelectLetter @valueLetter="getValueLetter" />
        <div class="filterGenre">
            <h3>Filtra per genere</h3>
            <select name="filterSeries" id="filterSeries" @click="getValueOption">
                <option value="">Seleziona un genere</option>
                <!-- recupera le informazioni dall'api e popola le option -->
                <option v-for="genre in genreSeries" :key="genre.id" :value="genre.id">{{genre.name}}</option>
            </select>
        </div>
        <div>
            <!-- Mostra le cards in base alla ricerca del genere che abbiamo richiesto -->
            <div class="containerCard" v-if="genreSelected === ''">
                <CardSeries v-for="(cardSerie, index) in dataArr" :key="cardSerie.index" :cardSeriesData="cardSerie"
                    :indexSeriesData="(index + 20)" />
            </div>
            <div class="containerCard" v-else>
                <CardSeries v-for="(cardSerie, index) in searchGenre()" :key="cardSerie.index"
                    :cardSeriesData="cardSerie" :indexSeriesData="(index + 20)" />
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";
import { apiKey } from "@/env/apiKey";

import SelectLetter from './selectLetter.vue';
import CardSeries from './cardSeries.vue';

export default {
    name: 'seriesHome',
    data() {
        return {
            query: '',
            dataArr: [],
            genreSeries: [],
            genreSelected: '',
            preferred: []
        }
    },
    components: {
        SelectLetter,
        CardSeries
    },
    methods: {
        searchGenre() {
            let newArr = [];
            // se la serie non è presente nell'array lo aggiunge
            this.dataArr.forEach(serie => {
                if (serie.genre_ids.includes(parseInt(this.genreSelected))) {
                    newArr.push(serie);
                }
            });
            return newArr;
        },
        getValueLetter(value) {
            this.query = value;
            this.dataArr = this.getApiDataHomepage(this.query);
        },
        getValueOption() {
            this.genreSelected = document.getElementById('filterSeries').value;
        },
        getApiDataHomepage(query) {
            let arr = [];

            // Genero una chiamata ad axios per ottenere i dati da un API.
            // L'url di seguito ha la query esterna in quanto verrà modificata dall'utente in base alla ricerca dei film che vorrà eseguire
            axios
                .get(
                    `https://api.themoviedb.org/3/search/tv?api_key=${apiKey}&language=it-IT&page=1&include_adult=false&query=${query}`
                )
                .then(({ data, status }) => {
                    if (status === 200) {
                        // Assegno i dati contenuti nell'array di oggetti contenuto nell'API alla variabile globale di tipo Array
                        arr.push(...data.results);
                        this.maxPage += parseInt(data.total_pages);
                    }
                })
                .catch((e) => {
                    e.message;
                });

            return arr;
        },
        getApiGenre() {
            // Recupera i generi dall'api
            let genre = [];

            axios
                .get(
                    `https://api.themoviedb.org/3/genre/tv/list?api_key=${apiKey}&language=it-IT`
                )
                .then(({ data, status }) => {
                    if (status === 200) {
                        // Assegno i dati contenuti nell'array di oggetti contenuto nell'API alla variabile globale di tipo Array
                        genre.push(...data.genres);
                    }
                })
                .catch((e) => {
                    e.message;
                });

            return genre;
        }
    },
    mounted() {
        this.dataArr = this.getApiDataHomepage("A");
        this.genreSeries = this.getApiGenre();
    }
}
</script>

<style lang="scss" scoped>
.titleSeries {
    width: 100%;

    #jumbo {
        width: 100%;
        height: 400px;
        position: relative;

        img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            filter: brightness(0.4);
        }

        #jumboText {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 50%;
            color: #fff;
            font-size: 3rem;
            text-align: center;
        }
    }

    span {
        margin: 40px 40px 15px;
        display: flex;
        justify-content: center;
        align-items: center;
        color: #fff;

        #logo {
            height: 50px;
            padding-left: 10px;
        }
    }

}

.filterGenre {
    color: #fff;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    padding: 20px 30px;

    select {
        margin: 0 30px;
        width: 200px;
        height: 30px;
        padding: 0 10px;
        background-color: #000;
        color: #fff;
    }
}

.containerCard {
    display: flex;
    flex-wrap: wrap;
    padding: 10px 30px 50px;
}
</style>