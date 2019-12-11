<script>
  import SearchBox from './SearchBox.svelte';
  import ResultsBox from './ResultsBox.svelte';

  let searchTerm = '';
  let searchData = {
    status: 'INITIAL',
    results: [],
  };

  const fetchData = (event) => {
    searchData = {
      status: 'FETCHING',
      results: [],
    };

    fetch(`https://en.wikipedia.org/w/api.php?action=query&list=search&srsearch=${searchTerm}&format=json&origin=*`)
    .then(data => data.json())
    .then(data => {
      searchData = {
        status: 'FETCHED',
        results: data.query.search,
      };
    })
    .catch(err => {
      searchData = {
        status: 'ERROR',
        results: [],
      };
    });
  };
</script>

<style>
a {
  text-decoration: underline;
}

.hero-body {
  display: flex;
  justify-content: center;
  flex-direction: column;
}

#search-box-wrapper {
  user-select: none;
  margin: 10px;
}
</style>

<section class="hero is-fullheight is-light is-bold">
  <div class="hero-body">
    <div id="search-box-wrapper" class="container is-fluid is-centered has-text-centered">
      <h1 class="title is-4"> Wikipedia Viewer </h1>
      <p class="subtitle is-6"> Search for an article, or get a random one <a href="https://en.wikipedia.org/wiki/Special:Random" target="_blank">here</a>.</p>
      <SearchBox bind:searchTerm={searchTerm} on:submit={fetchData}/>
    </div>
    <div class="container is-fluid">
      <div class="columns is-multiline">
        <ResultsBox searchData={searchData}/>
      </div>
    </div>
  </div>
</section>