<template>
    <div class="bg-page">
        <div class="containerArea">
            <div class="boxData">
                <h2>Nessun dato presente</h2>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'myList',
}
</script>

<style lang="scss" scoped>
.containerArea {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;

    .boxData {
        border: 3px solid rgb(119, 119, 119);
        background-color: rgb(37, 37, 37);
        width: 70%;
        height: 80%;
        border-radius: 20px;
        color: #fff;
        display: flex;
        justify-content: center;
        align-items: center;
    }
}
</style>