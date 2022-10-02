<template>
    <div>
        <div class="selectLetter">
            <ul>
                <li class="noSelect">-</li>
                <li id="0" class="firstLetter active" @click="getValue('0')">A</li>
                <li :id="index + 1" @click="getValue(index + 1)" v-for="(letter, index) in alphabet" :key="index + 1">
                    {{letter}}
                </li>
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
            alphabet: ['B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'L',
                'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'Z'],
        }
    },
    methods: {
        getValue(i) {

            document.querySelector(".firstLetter").classList.remove("active");
            for (let index = 0; index < this.alphabet.length; index++) {
                document.getElementById(`${index + 1}`).classList.remove("active");
            }

            document.getElementById(`${i}`).classList.add("active");
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

        .active {
            color: #fff;
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