<template>
    <!-- Essendo un array di 40 elementi dove i primi 20 sono le series e i restanti 20 sono movies,
         itero l'intero array facendo passare i primi 20 in questa sezione e gli altri nella sezione dei movies -->
    <div class="card" v-if="indexSeriesData > 19">
        <img id="poster" :src="getPosterPath('w342', cardSeriesData.poster_path)" :alt="cardSeriesData.title"
            @error="changeImgPoster" />

        <div class="areaDescription">
            <!-- Se il titolo è uguale al titolo originale ne mostrerà solo 1 -->
            <div v-if="cardSeriesData.name === cardSeriesData.original_name">
                <p v-if="cardSeriesData.name!= ''">Titolo: {{ cardSeriesData.name }}</p>
                <p v-else>Titolo: Dato non presente</p>
            </div>
            <div v-else>
                <p v-if="cardSeriesData.name!= ''">Titolo: {{ cardSeriesData.name }}</p>
                <p v-else>Titolo: Dato non presente</p>
                <p v-if="cardSeriesData.original_name!= ''">Titolo originale: {{ cardSeriesData.original_name }}</p>
                <p v-else>Titolo originale: Dato non presente</p>
            </div>

            <p>Language:
                <img :src="setFlagIcon(cardSeriesData.original_language)" :alt="cardSeriesData.original_language"
                    @error="changeImg" />
            </p>

            <div>
                <!-- L'area voto con le stelle mostra le stelle in base alla votazione che ha ricevuto il film -->
                <p id="vote">Vote:
                    <span v-if="cardSeriesData.vote_average != ''">
                        <StarVoted :starValue="toFiveStars(cardSeriesData.vote_average)" />
                    </span>
                    <span v-else>Dato non presente</span>
                </p>
            </div>
            <p v-if="cardSeriesData.overview != ''">Trama: {{cardSeriesData.overview}}</p>
            <p v-else>Trama: Dato non presente</p>
        </div>
    </div>
</template>

<script>
import StarVoted from './starVoted.vue';

export default {
    name: "cardSeries",
    props: {
        cardSeriesData: Object,
        indexSeriesData: Number
    },
    methods: {
        // funzione per mostrare un solo titolo o il titolo originale e quello tradotto
        viewOneTitle(translatedTitle, originalTitle) {
            if (translatedTitle === originalTitle) {
                return `Titolo: ${translatedTitle}`;
            }
            else {
                return `Titolo: ${translatedTitle}
        Titolo Originale: ${originalTitle}`;
            }
        },
        // converte il voto presente nell'array in un numero arrotondato per difetto che va da 1 a 5
        toFiveStars(vote) {
            return Math.ceil(vote / 2);
        },
        getPosterPath(size, posterPath) {
            return `https://image.tmdb.org/t/p/${size}${posterPath}`;
        },
        // sostituisce le immagini delle bandiere non presenti nell'api
        setFlagIcon(country) {
            switch (country) {
                case "en":
                    country = "GB";
                    break;
                case "ja":
                    country = "jp";
                    break;
            }
            return ("https://www.countryflagicons.com/FLAT/32/" +
                country.toUpperCase() +
                ".png");
        },
        changeImg(e) {
            e.target.src = "https://w7.pngwing.com/pngs/655/930/png-transparent-false-error-missing-absent-x-red-cross-letter-circle-gui-thumbnail.png";
        },
        changeImgPoster(e) {
            e.target.src = "https://upload.wikimedia.org/wikipedia/commons/thumb/6/65/No-Image-Placeholder.svg/1665px-No-Image-Placeholder.svg.png";
        }
    },
    components: {
        StarVoted
    }
}
</script>

<style lang="scss" scoped>
.card {
    height: 515px;
    position: relative;
    margin: 10px auto;
    text-align: center;

    #poster {
        min-width: 342px;
        max-width: 342px;
        height: 100%;
        object-fit: cover;
    }

    &:hover .areaDescription {
        display: inline-block;
    }

    .areaDescription {
        display: none;
        position: absolute;
        top: 0px;
        left: 0px;
        padding: 40px 30px;
        width: 100%;
        height: 100%;
        color: #fff;
        background-color: rgba(0, 0, 0, 0.7);
        overflow: hidden;
        border: 8px double rgb(92, 92, 92);
        box-shadow: 0px 0px 100px #000000 inset;
        z-index: 10;

        &:hover {
            overflow-y: auto;
        }
    }

    .areaDescription img {
        width: 32px;
        position: relative;
        top: 10px;
        left: 10px;
    }

    p {
        text-align: left;
        padding-bottom: 10px;
    }

    #vote {
        padding-top: 10px;
    }

    .title p:nth-child(1) {
        font-size: 1.5rem;
        padding-bottom: 20px;
    }
}
</style>