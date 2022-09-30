<template>
    <div class="card" v-if="indexSeriesData > 19">
        <img id="poster" :src="getPosterPath('w342', cardSeriesData.poster_path)" :alt="cardSeriesData.title"
        @error="changeImgPoster"/>
        
        <div class="areaDescription">
            <div v-if="cardSeriesData.name === cardSeriesData.original_name">
                <p>Titolo Serie: {{ cardSeriesData.name }}</p>
            </div>
            <div v-else>
                <p>Titolo Serie: {{ cardSeriesData.name }}</p>
                <p>Titolo Originale: {{ cardSeriesData.original_name }}</p>
            </div>

            <p>Language:
                <img :src="setFlagIcon(cardSeriesData.original_language)" :alt="cardSeriesData.original_language"
                @error="changeImg"/>
            </p>

            <div>
                <p id="vote">Vote:
                    <span v-if="toFiveStars(cardSeriesData.vote_average) === 1">
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                    </span>
                    <span v-else-if="toFiveStars(cardSeriesData.vote_average) === 2">
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                    </span>
                    <span v-else-if="toFiveStars(cardSeriesData.vote_average) === 3">
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                    </span>
                    <span v-else-if="toFiveStars(cardSeriesData.vote_average) === 4">
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starGray fa-regular fa-star"></i>
                    </span>
                    <span v-else-if="toFiveStars(cardSeriesData.vote_average) === 5">
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                        <i class="starYellow fa-solid fa-star"></i>
                    </span>
                </p>
            </div>
            <p>{{cardSeriesData.overview}}</p>
        </div>
        <i id="showMoreInfo" class="fa-solid fa-circle-arrow-right"></i>
    </div>
</template>

<script>
export default {
    name: 'cardMovies',
    props: {
        cardSeriesData: Object,
        indexSeriesData: Number
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

    #showMoreInfo {
        display: none;
    }

    &:hover #showMoreInfo {
        display: inline-block;
        font-size: 1.8rem;
        position: absolute;
        bottom: 30px;
        color: #fff;
        animation: backAndForth linear 0.85s infinite;
        cursor: pointer;

        &:hover{
            color: rgb(209, 209, 209);
        }
    }

    @keyframes backAndForth {
            0% {
                right: 15%
            }

            ;

            50% {
                right: 10%
            }

            ;

            100% {
                right: 15%
            }

            ;
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