<script>
  export let searchTerm;
</script>

<form class="form" on:submit|preventDefault>
  <div class="field">
    <div class="control">
      <input type="text" class="input is-large is-rounded is-primary" placeholder="Enter a search term." bind:value={searchTerm}>
    </div>
  </div>
</form>