<template>
    <div class="detail">
        <div class="detail_view" v-if="show"></div>
        <font-awesome-icon icon="spinner" class="icon" />
    </div>
</template>

<script>
export default {
    props: {
        pokemonUrl: String,
        imageUrl: String
    },
    data() {
        return {
            show: false,
            pokemon: {}
        };
    },
    methods: {
        fetchData() {
            axios
                .get(this.pokemonUrl)
                .then(res => {
                    this.pokemon = res;
                    this.show = true;
                })
                .catch(err => {
                    console.log(err);
                });
        }
    },
    created() {
        this.fetchData();
    }
};
</script>

<style lang="scss" scoped>
.detail {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    flex-direction: column;
    position: fixed;
}
</style>
