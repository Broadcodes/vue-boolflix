<template>
    <div class="card" v-if="indexMoviesData < 20">
        <img id="poster" :src="getPosterPath('w342', cardMoviesData.poster_path)" :alt="cardMoviesData.title"
        @error="changeImgPoster"/>
        <div class="areaDescription">

            <div v-if="cardMoviesData.title === cardMoviesData.original_title">
                <p>Titolo Movie: {{ cardMoviesData.title }}</p>
            </div>
            <div v-else>
                <p>Titolo Movie: {{ cardMoviesData.title }}</p>
                <p>Titolo Originale: {{ cardMoviesData.original_title }}</p>
            </div>

            <p>Language:
                <img :src="setFlagIcon(cardMoviesData.original_language)" :alt="cardMoviesData.original_language" 
                @error="changeImg"/>
            </p>

            <div>
                <p id="vote">Vote:
                    <span v-if="toFiveStars(cardMoviesData.vote_average) === 1">
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                    </span>
                    <span v-else-if="toFiveStars(cardMoviesData.vote_average) === 2">
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                    </span>
                    <span v-else-if="toFiveStars(cardMoviesData.vote_average) === 3">
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                    </span>
                    <span v-else-if="toFiveStars(cardMoviesData.vote_average) === 4">
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                    </span>
                    <span v-else-if="toFiveStars(cardMoviesData.vote_average) === 5">
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                    </span>
                </p>
            </div>
            <p>{{cardMoviesData.overview}}</p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'cardMovies',
    props: {
        cardMoviesData: Object,
        indexMoviesData: Number
    },
    methods: {
        viewOneTitle(translatedTitle, originalTitle) {

            if (translatedTitle === originalTitle) {
                return `Titolo: ${translatedTitle}`;
            } else {
                return `Titolo: ${translatedTitle}
        Titolo Originale: ${originalTitle}`;
            }
        },
        toFiveStars(vote) {
            return Math.ceil(vote / 2);
        },
        getPosterPath(size, posterPath) {
            return `https://image.tmdb.org/t/p/${size}${posterPath}`;
        },
        setFlagIcon(country) {
            switch (country) {
                case "en":
                    country = "GB";
                    break;
                case "ja":
                    country = "jp";
                    break;
            }
            return (
                "https://www.countryflagicons.com/FLAT/32/" +
                country.toUpperCase() +
                ".png"
            );
        },
        changeImg(e){
            e.target.src = "https://w7.pngwing.com/pngs/655/930/png-transparent-false-error-missing-absent-x-red-cross-letter-circle-gui-thumbnail.png";
        },
        changeImgPoster(e){
            e.target.src = "https://upload.wikimedia.org/wikipedia/commons/thumb/6/65/No-Image-Placeholder.svg/1665px-No-Image-Placeholder.svg.png";
        }
    },
}
</script>

<style lang="scss" scoped>
.card {
    height: 515px;
    position: relative;
    margin: 10px auto;
    text-align: center;

    #poster{
        min-width: 342px;
        max-width: 342px;
        height: 100%;
        object-fit: cover;
    }

    &:hover .areaDescription{
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

    .starYellow {
        color: rgb(238, 202, 42);
    }

    .starGray {
        color: rgb(199, 199, 199);
    }
}
</style>