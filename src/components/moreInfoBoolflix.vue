<template>
    <div>
        <!-- Area raffiguranti le sezioni presenti nella homepage -->
        <div class="container">
            <div class="containerArea firstArea">
                <div class="text1">
                    <h2>Goditi Boolflix sulla tua TV</h2>
                    <h3>Guarda Boolflix su smart TV, Playstation, Xbox, Chromecast, Apple TV, lettori Blu-ray e molti
                        altri
                        dispositivi.</h3>
                </div>
                <div class="image1">
                    <img src="@/assets/img/tv.png" alt="tv image">
                    <video id="video1" autoplay muted>
                        <source src="@/assets/img/video.mp4" type="video/mp4">
                    </video>
                </div>
            </div>
            <div class="containerArea secondArea">
                <div class="image2">
                    <img src="@/assets/img/mobile.jpg" alt="mobile">
                </div>
                <div class="text2">
                    <h2>Scarica le tue serie da guardare offline.</h2>
                    <h3>Salva facilmente i tuoi preferiti così avrai sempre qualcosa da guardare.</h3>
                </div>
            </div>
            <div class="containerArea thirdArea">
                <div class="text1">
                    <h2>Guarda Boolflix ovunque.</h2>
                    <h3>Cellulare, tablet, laptop e TV: scegli tu cosa usare per guardare in streaming film e serie TV
                        senza limiti e senza spendere di più.</h3>
                </div>
                <div class="image3">
                    <img src="@/assets/img/device-pile.png" alt="device image">
                    <video id="video3" autoplay muted>
                        <source src="@/assets/img/video-devices.mp4" type="video/mp4">
                    </video>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'moreInfoBoolflix'
}
</script>

<style lang="scss" scoped>
.container {
    background-color: #000;
    width: 100%;
    box-shadow: 0px 0px 30px rgb(168, 168, 168);

    .containerArea {
        width: 100%;
        height: 500px;
        border-top: 5px solid rgb(94, 94, 94);
        border-bottom: 5px solid rgb(94, 94, 94);
    }

    .firstArea,
    .secondArea,
    .thirdArea {
        display: flex;
    }

    .text1,
    .text2,
    .text3 {
        flex-basis: 60%;
        color: #fff;
        padding: 100px 100px 100px 200px;
        justify-self: center;
        align-self: center;

        h2 {
            font-size: 3rem;
            padding: 20px 0;
        }

        h3 {
            font-size: 1.5rem;
            line-height: 2rem;
        }
    }

    .image1,
    .image3 {
        flex-grow: 1;
        position: relative;

        img {
            position: relative;
            height: 100%;
            padding: 40px 0;
            z-index: 4;
        }

        #video1 {
            position: absolute;
            top: 120px;
            left: 70px;
            width: 400px;
            z-index: 3;
        }

        #video3 {
            position: absolute;
            top: 100px;
            left: 90px;
            width: 360px;
            z-index: 3;
        }
    }


    .text2 {
        flex-basis: 55%;
        padding-left: 50px;
    }

    .image2 {
        flex-grow: 1;
        display: flex;
        justify-content: flex-end;

        img {
            height: 100%;
        }
    }

}
</style>