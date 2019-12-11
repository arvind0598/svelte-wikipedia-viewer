<script>
import { afterUpdate } from 'svelte';
import SingleResult from './SingleResult.svelte';
import Loader from './Loader.svelte';

export let searchData = {};
let results = [];

afterUpdate(() => {
  results = searchData.results;
});
</script>

{#if searchData.status === 'FETCHED'}
  {#if searchData.results.length > 0}
    {#each results as data, i}
      <div class="column is-3">
        <SingleResult caption={data.title} snippet={data.snippet} pageid={data.pageid} delay={i * 50}/>
      </div>
    {/each}
  {:else}
    <p class="title is-4 has-text-centered"> There were no results returned.</p>
  {/if}
{:else if searchData.status === 'FETCHING'}
  <Loader/>
{:else if searchData.status === 'ERROR'}
  <p class="title is-4 has-text-centered"> There was an error in fetching the data.</p>
{/if}