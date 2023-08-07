<script>
    export let movies;
</script>

{#each movies as movie}
<h2>{movie.title}</h2>
<p>{movie.overview}</p>
{/each}