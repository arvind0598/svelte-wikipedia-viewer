<script>
  export let title = 'DEFAULT';
  export let snippet = '';
</script>

<div class="message">
  <div class="message-header">
    {title}
  </div>
  <div class="message-body">
    {@html snippet}
  </div>
</div>