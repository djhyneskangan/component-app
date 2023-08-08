<script>
    import NewEntry from "./newEntry.svelte";

    let newEntry = 'No Entry yet';
    let entries = [];

    function handleNewEntry(event) {
        console.log(event.detail.text);
        newEntry = event.detail.text;

        entries = [...entries, newEntry];
    }
</script>ß

Journal Entries

{newEntry}

<ol>
{#each entries as entry}
    <li>{entry}</li>
{/each}
</ol>
<div>
    <NewEntry on:newEntry={handleNewEntry}/>
</div>