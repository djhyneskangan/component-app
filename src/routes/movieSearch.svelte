<!-- src/routes/Search.svelte -->
<script>
    import { onMount } from 'svelte';
    import { createEventDispatcher } from 'svelte';
    import { Search } from 'flowbite-svelte'
    import { Button } from 'flowbite-svelte'
    //import JournalEntries from './journalEntries.svelte';

    import MovieCard from './movieCard.svelte';
	import NewEntry from './newEntry.svelte';
       
     const dispatch = createEventDispatcher();
     let searchTerm = '';
     let searchResults = [];
  
    async function fetchMovies(query) {
      if (!query) {
        searchResults = [];
        return; 
      }
  
      const apiKey = '5b93bc2a6a4897a2c7b5cb399f067bac'; // Replace 'YOUR_API_KEY' with your actual TMDb API key.
      const url = `https://api.themoviedb.org/3/search/movie?api_key=${apiKey}&query=${query}`;
  
      try {
        const response = await fetch(url);
        const data = await response.json();
        searchResults = data.results;
        console.log(data)
      } catch (error) {
        console.error('Error fetching data:', error);
        searchResults = [];
      }
    }
  
    function handleSubmit(event) {
      event.preventDefault();
      fetchMovies(searchTerm);
    }
  
    onMount(() => {
      fetchMovies(''); // Fetch data on initial load (you can modify this if needed).
    });
  </script>
  

  <form class="flex gap-2 max-w-xs content-center" on:submit={handleSubmit}>
    <Search size="md" input
    type="text"
    bind:value={searchTerm}
    placeholder="Search movies..." />
    <Button class="!p-2.5" type="submit">
      <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"/></svg>
    </Button>
  </form>

  <JournalEntries />

    <h2>Results:</h2>
    
{#if searchResults.length === 0}
<p>No results found.</p>
{:else}
<div class="flex flex-wrap justify-center content-between object-contain gap-4 pl-8 pr-8">
  {#each searchResults as movie}
    <div class="group h-96 w-64 [perspective:1000px] flex-initial">
      <div class="relative h-full w-full rounded-xl shadow-xl transition-all duration-1000 [transform-style:preserve-3d] group-hover:[transform:rotateY(180deg)]">
        <div class="absolute inset-0">
            {#if movie.poster_path === null}
          <img class="h-full w-full rounded-xl shadow-xl shadow-black/40 flex-auto" src="./src/lib/images/no_image_available.svg" alt="{movie.title}" />
            {:else}
            <img class="h-full w-full rounded-xl shadow-xl shadow-black/40 flex-auto" src="{'https://image.tmdb.org/t/p/w400' + movie.poster_path}" alt="{movie.title}" />
            {/if}
        </div>
        <div class="absolute inset-0 h-full w-full rounded-xl bg-black/80 px-12 text-center text-slate-200 [transform:rotateY(180deg)] [backface-visibility:hidden]">
          <div class="flex min-h-full flex-col items-center justify-center">
            <h2 class="text-lg font-bold">{movie.title}</h2>
            {#if movie.release_date === ""}
            <p class="text-xs">No Available Release Date</p>
            {:else}
                <p>({movie.release_date.split("-")[0]})</p>
            {/if}
                <Button class="mt-6">More Info</Button>
          </div>
        </div>
      </div>
    </div>
  {/each}
</div>
{/if}