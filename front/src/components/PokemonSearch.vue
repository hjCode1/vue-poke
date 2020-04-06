<template>
    <div class="searchbar">
        <form @submit.prevent="setPokemonUrl">
            <input type="text" placeholder="Please enter a number" v-model="searchValue" />
        </form>
        <font-awesome-icon icon="search" class="btn_search" @click="setPokemonUrl" />
    </div>
</template>

<script>
export default {
    props: {
        apiUrl: String
    },
    data() {
        return {
            searchValue: ''
        };
    },
    methods: {
        setPokemonUrl(url) {
            if (this.searchValue !== '') {
                this.$emit('setPokemonUrl', this.apiUrl + '/' + this.searchValue);
            }
        }
    }
};
</script>

<style lang="scss" scoped>
.searchbar {
    position: relative;
    width: 100%;
    max-width: 510px;
    padding-bottom: 20px;

    input {
        border: none;
        outline: none;
        border-radius: 5px;
        padding: 10px 40px 10px 10px;
        width: calc(100% - 50px);
        font-size: 1rem;
        box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
    }

    .btn_search {
        position: absolute;
        right: 10px;
        top: 10px;
        font-size: 1.25rem;
        color: #0a2e50;
        cursor: pointer;
    }
}
</style>
