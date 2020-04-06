<template>
    <div class="list">
        <article v-for="(pokemon, index) in pokemons" :key="'poke' + index" @click="setPokemonUrl(pokemon.url)">
            <img :src="imageUrl + pokemon.id + '.png'" alt width="96" height="96" />
            <h3>{{ pokemon.name }}</h3>
        </article>
        <div id="scroll_trigger" ref="infiniteScroll">
            <font-awesome-icon icon="spinner" class="icon" />
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    props: {
        imageUrl: String,
        apiUrl: String
    },
    data() {
        return {
            pokemons: [],
            nextUrl: '',
            currentUrl: ''
        };
    },
    methods: {
        fetchData() {
            axios
                .get(this.currentUrl)
                .then(res => {
                    const { next, results } = res.data;

                    this.nextUrl = next;
                    results.forEach(pokemon => {
                        pokemon.id = pokemon.url
                            .split('/')
                            .filter(function(part) {
                                return !!part;
                                // part 는 https pokeapi api ...
                                // 여기서 마지막 true값은 숫자임
                                // 마지막 숫자를 반환
                            })
                            .pop();
                        this.pokemons.push(pokemon);
                    });
                })
                .catch(err => {
                    console.log(err);
                });
        },
        scrollTrigger() {
            const io = new IntersectionObserver(entries => {
                entries.forEach(entry => {
                    if (entry.isIntersecting && this.nextUrl) {
                        this.next();
                    }
                });
            });
            io.observe(this.$refs.infiniteScroll);
        },
        next() {
            this.currentUrl = this.nextUrl;
            this.fetchData();
        },
        setPokemonUrl(url) {
            console.log('set poke: ', url);
            this.$emit('setPokemonUrl', url);
        }
    },
    created() {
        this.currentUrl = this.apiUrl;
        this.fetchData();
    },
    mounted() {
        this.scrollTrigger();
    }
};
</script>

<style lang="scss" scoped>
.list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    grid-gap: 10px;
    width: 100%;
    max-width: 510px;

    article {
        height: 150px;
        background: #efefef;
        text-align: center;
        text-transform: capitalize;
        border-radius: 5px;
        cursor: pointer;
        box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);

        h3 {
            margin: 0;
        }
    }
}
#scroll_trigger {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 150px;
    font-size: 2rem;
    color: #efefef;
}
</style>
