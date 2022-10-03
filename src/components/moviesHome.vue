<template>
    <div class="bg-page">
        <!-- Pagina che mostra solo i movies. Raggiungibile dalla homepage cliccando nella barra di navigazione header -->
        <div class="titleSeries">
            <div id="jumbo">
                <img src="@/assets/img/seriesPoster.png" alt="seriesPoster">
                <h2 id="jumboText">I miglior film da guardare in compagnia e non...
                    per un'esperienza unica nel suo genere!</h2>
            </div>
            <span>
                <h1>Tutti i miglior film solo su</h1>
                <img id="logo" src="@/assets/img/boolflix_logo.png" alt="boolflix logo">
            </span>
        </div>
        <!-- Permette di effettuare delle ricerche in base alla lettera selezionata -->
        <SelectLetter @valueLetter="getValueLetter" />
        <div class="filterGenre">
            <h3>Filtra per genere</h3>
            <!-- Permette di effettuare delle ricerche in base al genere selezionato -->
            <select name="filterMovies" id="filterMovies" @click="getValueOption">
                <option value="">Seleziona un genere</option>
                <option v-for="genre in genreMovies" :key="genre.id" :value="genre.id">{{genre.name}}</option>
            </select>
        </div>
        <div>
            <div class="containerCard" v-if="genreSelected === ''">
                <CardMovies v-for="(cardMovie, index) in dataArr" :key="cardMovie.index" :cardMoviesData="cardMovie"
                    :indexMoviesData="index" />
            </div>
            <div class="containerCard" v-else>
                <CardMovies v-for="(cardMovie, index) in searchGenre()" :key="cardMovie.index"
                    :cardMoviesData="cardMovie" :indexMoviesData="index" />
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";
import { apiKey } from "@/env/apiKey";

import SelectLetter from './selectLetter.vue';
import CardMovies from "./cardMovies.vue";

export default {
    name: 'moviesHome',
    components: {
        SelectLetter,
        CardMovies
    },
    data() {
        return {
            query: '',
            genreSelected: '',
            dataArr: [],
            genreMovies: [],
        }
    },
    methods: {
        searchGenre() {
            let newArr = [];

            this.dataArr.forEach(movie => {
                if (movie.genre_ids.includes(parseInt(this.genreSelected))) {
                    newArr.push(movie);
                }
            });
            return newArr;
        },
        getValueLetter(value) {
            this.query = value;
            this.dataArr = this.getApiDataHomepage(this.query);
        },
        getValueOption() {
            this.genreSelected = document.getElementById('filterMovies').value;
        },
        getApiDataHomepage(query) {
            let arr = [];

            // Genero una chiamata ad axios per ottenere i dati da un API.
            // L'url di seguito ha la query esterna in quanto verrà modificata dall'utente in base alla ricerca dei film che vorrà eseguire
            axios
                .get(
                    `https://api.themoviedb.org/3/search/movie?api_key=${apiKey}&language=it-IT&page=1&include_adult=false&query=${query}`
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
            let genre = [];

            axios
                .get(
                    `https://api.themoviedb.org/3/genre/movie/list?api_key=${apiKey}&language=it-IT`
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
        this.genreMovies = this.getApiGenre();
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