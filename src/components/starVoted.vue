<template>
    <div>
        <!-- restituisce le stelle per indicare il voto del film o della serie -->
        <span v-if="starValue === 1">
            <i class="starYellow fa-solid fa-star"></i>
            <i class="starGray fa-regular fa-star"></i>
            <i class="starGray fa-regular fa-star"></i>
            <i class="starGray fa-regular fa-star"></i>
            <i class="starGray fa-regular fa-star"></i>
        </span>
        <span v-else-if="starValue === 2">
            <i class="starYellow fa-solid fa-star"></i>
            <i class="starYellow fa-solid fa-star"></i>
            <i class="starGray fa-regular fa-star"></i>
            <i class="starGray fa-regular fa-star"></i>
            <i class="starGray fa-regular fa-star"></i>
        </span>
        <span v-else-if="starValue === 3">
            <i class="starYellow fa-solid fa-star"></i>
            <i class="starYellow fa-solid fa-star"></i>
            <i class="starYellow fa-solid fa-star"></i>
            <i class="starGray fa-regular fa-star"></i>
            <i class="starGray fa-regular fa-star"></i>
        </span>
        <span v-else-if="starValue === 4">
            <i class="starYellow fa-solid fa-star"></i>
            <i class="starYellow fa-solid fa-star"></i>
            <i class="starYellow fa-solid fa-star"></i>
            <i class="starYellow fa-solid fa-star"></i>
            <i class="starGray fa-regular fa-star"></i>
        </span>
        <span v-else-if="starValue === 5">
            <i class="starYellow fa-solid fa-star"></i>
            <i class="starYellow fa-solid fa-star"></i>
            <i class="starYellow fa-solid fa-star"></i>
            <i class="starYellow fa-solid fa-star"></i>
            <i class="starYellow fa-solid fa-star"></i>
        </span>
    </div>
</template>

<script>
export default {
    name: 'starVoted',
    props: {
        starValue: Number
    },
}
</script>

<style lang="scss" scoped>
.starYellow {
    color: rgb(238, 202, 42);
}

.starGray {
    color: rgb(199, 199, 199);
}
</style>