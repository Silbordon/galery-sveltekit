<script lang="ts">
import Card from "../components/Card.svelte";
import Loading from "../components/Loading.svelte";


let actualPage:number =1;
let searchParams:string = "";
let ref:any;

const apiKey = "bH81tUFHG-g-zQDZR895aKT_Tto5iH7eowv6SGQLTaI"
const getImages = async(page:number=1, searchParams="park") =>{
    if(searchParams.trim() === ""){
        return
    }

    const res = await fetch(` https://api.unsplash.com/search/collections/?query=${searchParams}&page=${page}&per_page=${12}&client_id=${apiKey}`) 
    const data = await res.json()
    return data
}

let promise = getImages()

const handleSubmit = (e : any) =>{
    actualPage = 1
    promise = getImages(actualPage,searchParams)
}

const handleNextPage = () =>{
    actualPage ++;
    promise = (getImages(actualPage, searchParams ))
}

const handlePrevPage = () =>{
    actualPage --;
    promise = (getImages(actualPage, searchParams))
}

</script>


<svelte:head>
    <title>Search {searchParams.trim()== "" ? "" : `- ${searchParams} Page ${actualPage}`}</title>
</svelte:head>

<form on:submit|preventDefault={handleSubmit} class="form-group row">
    <div class="col-12 col-md-8">
            <input
                bind:value={searchParams}
                bind:this={ref}
                type="text" 
                placeholder="Search Params" 
                class="form-control"
                on:focus={()=>ref.select()}
            >
                
    </div>
    <div class="col-12 col-md-4">
        <button class="btn btn-dark" type="submit">Search</button>
    </div>
</form>

<div class="text-center">
    {#await promise}
    <Loading/>
{:then data} 
<div class="row g-3">
    {#each data.results as image }
    <div class="col-12 col-md-4">
    <Card 
        url={image.cover_photo.urls.thumb}
        title={image.cover_photo.alt_description}
        download={image.cover_photo.urls.full}
    />
    </div>
 {/each}
    </div>
    {#if actualPage !== 1}
        <button on:click={handlePrevPage} class="btn btn-warning">Prev</button>

    {/if}
    <button on:click={handleNextPage} class="btn btn-info">Next</button>
{/await}
</div>
    
