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
    {#each results as data(data.id)}
      <div class="column is-half">
        <SingleResult title={data.title} snippet={data.snippet}/>
      </div>
    {/each}
  {/if}
{/if}