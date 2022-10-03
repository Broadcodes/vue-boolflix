<template>
    <div>
        <div class="componentArea">
            <ul>
                <li><a href="#">Domande frequenti</a></li>
                <li><a href="#">Rapporti con gli investitori</a></li>
                <li><a href="#">Come guardare Boolflix</a></li>
                <li><a href="#">Informazioni sull'azienda</a></li>
                <li><a href="#">Note legali</a></li>
            </ul>
            <ul>
                <li><a href="#">Centro assistenza</a></li>
                <li><a href="#">Opportunità di lavoro</a></li>
                <li><a href="#">Condizioni di utilizzo</a></li>
                <li><a href="#">Contattaci</a></li>
                <li><a href="#">Solo su Boolflix</a></li>
            </ul>
            <ul>
                <li><a href="#">Account</a></li>
                <li><a href="#">Riscatta carte regalo</a></li>
                <li><a href="#">Privacy</a></li>
                <li><a href="#">Test di velocità</a></li>
            </ul>
            <ul>
                <li><a href="#">Media center</a></li>
                <li><a href="#">Acquista carte regalo</a></li>
                <li><a href="#">Preferenza per i cookie</a></li>
                <li><a href="#">Garanzia legale</a></li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    name: 'footerComponent'
}
</script>

<style lang="scss" scoped>
.componentArea {
    width: 100%;
    height: 450px;
    display: flex;
    padding: 140px 100px;
    justify-content: space-evenly;
    align-items: top;

    ul {
        list-style-type: none;

        li {
            padding: 15px;

            a {
                text-decoration: none;
                color: rgb(121, 121, 121);
                font-size: 0.8rem;

                &:hover {
                    text-decoration: underline;
                }
            }
        }
    }
}
</style>