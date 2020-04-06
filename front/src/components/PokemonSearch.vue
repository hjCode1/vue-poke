<template>
    <div class="searchbar">
        <form @submit.prevent="setPokemonUrl">
            <input type="text" v-model="searchValue" />
        </form>
        <font-awesome-icon icon="search" @click="setPokemonUrl" />
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
                this.$emit('setPokemonUrl', this.apiUrl + this.searchValue);
            }
        }
    }
};
</script>

<style lang="scss" scoped></style>
