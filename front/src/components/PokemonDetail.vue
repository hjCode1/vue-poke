<template>
    <div class="detail">
        <div class="detail_view" v-if="show">
            <div class="image" v-if="pokemon">
                <img :src="imageUrl + pokemon.id + '.png'" alt="" />
            </div>
            <div class="data" v-if="pokemon">
                <h2>{{ pokemon.name }}</h2>
                <div class="property">
                    <div class="left">Base Experience</div>
                    <div class="right">{{ pokemon.base_experience }} XP</div>
                </div>
                <div class="property">
                    <div class="left">Height</div>
                    <div class="right">{{ pokemon.height / 10 }} m</div>
                </div>
                <div class="property">
                    <div class="left">Weight</div>
                    <div class="right">{{ pokemon.weight / 10 }} kg</div>
                </div>
                <h3>Pokemon Types</h3>
                <div class="types">
                    <div class="type" v-for="(value, index) in pokemon.types" :key="'value' + index">
                        {{ value.type.name }}
                    </div>
                </div>
            </div>
        </div>
        <font-awesome-icon v-else icon="spinner" class="icon" />
    </div>
</template>

<script>
import axios from 'axios';

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
                    this.pokemon = res.data;
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
    top: 0;
    left: 0;
    padding: 90px 10px 10px;
    width: calc(100% - 20px);
    height: calc(100vh - 20px);
    background: rgba(0, 0, 0, 0.2);

    .detail_view {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        position: relative;
        width: 100%;
        max-width: 510px;
        padding: 50px 0 0;
        background: #fff;
        border-radius: 5px;
        box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);

        .image {
            display: flex;
            justify-content: center;
            align-items: center;
            position: absolute;
            top: -60px;
            width: 120px;
            height: 120px;
            background: #333;
            border-radius: 50%;
            overflow: hidden;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
        }
        h2 {
            text-transform: capitalize;
        }
        .data {
            display: flex;
            justify-content: flex-start;
            align-items: center;
            flex-direction: column;
            width: 100%;
            margin-bottom: 40px;

            .property {
                width: 90%;
                max-width: 400px;
                border-bottom: 1px solid #ccc;
                margin-bottom: 10px;

                .left {
                    float: left;
                }
                .right {
                    float: right;
                }
            }
        }
    }
}
</style>
