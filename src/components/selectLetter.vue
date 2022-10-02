<template>
    <div>
        <div class="selectLetter">
            <ul>
                <li class="noSelect">-</li>
                <li @click="getValue(index)" v-for="(letter, index) in alphabet" :key="index">{{letter}}</li>
                <li class="noSelect">-</li>
            </ul>
            <span></span>
        </div>
    </div>
</template>

<script>
export default {
    name: 'selectLetter',
    data() {
        return {
            valueLetter: '',
            alphabet: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'L',
                'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'Z'],
        }
    },
    methods: {
        getValue(i) {
            this.valueLetter = this.alphabet[i];
            this.$emit('valueLetter', this.valueLetter);
        }
    }
}
</script>

<style lang="scss" scoped>
.selectLetter {
    color: rgb(128, 128, 128);
    font-size: 1.7rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 100%;
    padding: 40px;

    ul {
        list-style-type: none;
        display: flex;
        margin-bottom: 10px;

        li {
            margin: 0 20px;
            cursor: pointer;

            &:hover {
                color: #fff;
            }
        }

        .noSelect {
            cursor: default;
            color: rgb(128, 128, 128) !important;
        }
    }

    span {
        width: 100%;
        height: 5px;
        background: rgb(255, 255, 255);
        background: radial-gradient(circle, rgba(255, 255, 255, 0.123) 10%, rgba(23, 23, 23, 1) 85%);
    }
}
</style>