<script context="module">
    export async function load({fetch, params}){
        const id = params.id;
        const url = `https://pokeapi.co/api/v2/pokemon/${id}`; 
        const res = await fetch(url);
        const pokeman = await res.json(); 
        return {props: {pokeman}};
    }
</script>
<script>
    export let pokeman;
    let type = pokeman.types[0].type.name;
</script>

<div class="flex flex-col items-center">
    <h1 class="text-4xl text-center my-8 uppercase">{pokeman.name}</h1>
    <img class="card-image h-30 w-30" src={pokeman.sprites['front_default']} alt={pokeman.name}>
    <p>Type: <strong>{type.toUpperCase()}</strong> | Height: <strong>{pokeman.height}</strong> 
        | Weight: <strong>{pokeman.weight}</strong></p>
</div>
