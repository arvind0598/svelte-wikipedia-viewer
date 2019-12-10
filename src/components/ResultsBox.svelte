<script>
import { afterUpdate } from 'svelte';
import SingleResult from './SingleResult.svelte';

export let searchData = {};
let results = [];

afterUpdate(() => {
  console.log('update', searchData);
  results = searchData.results;
});
</script>

{#if searchData.status === 'FETCHED'}
  {#if searchData.results.length > 0}
    {#each results as data}
      <div class="column is-3">
        <SingleResult caption={data.title} snippet={data.snippet} pageid={data.pageid}/>
      </div>
    {/each}
  {/if}
{/if}