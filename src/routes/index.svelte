<script context="module">
    export async function load({fetch, params}){
        const url = `https://pokeapi.co/api/v2/pokemon?limit=150`;
        const res = await fetch(url);
        const data = await res.json();
        const loadedPokemon = data.results.map((data, index) => {
            return {
                name: data.name,
                id: index + 1,
                image: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index + 1}.png`
            };
        });
        return {props: {pokemon: loadedPokemon}};
    }
</script>

<script>
    import PokemanCard from '../components/pokemanCard.svelte';

    let searchTerm = "";
    let filteredPokemon = [];
    export let pokemon;

    const handleInput = () => {
    }

    //Updates pokemon list based on input text
    $ : {
        if (searchTerm){
           filteredPokemon = pokemon.filter(pokeman => pokeman.name.toLowerCase().includes(searchTerm.toLowerCase())); 
        } else {
            filteredPokemon = [...pokemon];
        } 
    } 
</script>

<svelte:head>
    <title>Svelte Kit Pokedex</title>
</svelte:head>

<h1 class="text-4xl text-center my-8 uppercase">SvelteKit Pokedex</h1>

<input class="w-full rounded-md text-lg p-4 border-2 border-gray-200" type="text" 
    bind:value={searchTerm} placeholder="Search Pokemon">

<div class="py-4 grid gap-4 md:grid-cols-2 grid-cols-1">
    {#each filteredPokemon as pokeman (pokeman.id)}
        <PokemanCard {pokeman}/>
    {/each}
</div>

