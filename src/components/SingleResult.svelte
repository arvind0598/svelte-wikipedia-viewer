<script>
  import { fade } from 'svelte/transition';
  import { afterUpdate } from 'svelte';

  export let caption = '';
  export let snippet = '';
  export let pageid = -1;

  let title = 'DEFAULT TITLE'
  let subtitle = 'DEFAULT SUBTITLE';

  afterUpdate(() => {
    const open = caption.indexOf('(');
    if (open < 0) {
      title = caption;
      subtitle = '';
      return;
    }

    const close = caption.indexOf(')');
    subtitle = caption.slice(open + 1, close);
    title = caption.slice(0, open);
  });

</script>

<style>
.card {
  height: 100%;
  display: flex;
  flex-direction: column;
  box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
  transition: 400ms ease all;
}

.card:hover {
  box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
}

.card-footer {
  margin-top: auto;
}
</style>

<div class="card">
  <div class="card-content">
    <div class="media">
      <div class="media-content">
        <p class="title is-3 has-text-black-bis"> {title} </p>
        <p class="subtitle is-5 has-text-dark"> <i>{subtitle}</i> </p>
      </div>
    </div>

    <div class="content">
    {@html snippet}...
    </div>
  </div>
  <footer class="card-footer">
    <a class="card-footer-item" href={`https://en.wikipedia.org/?curid=${pageid}`} target="_blank"> Visit </a>
  </footer>
</div>