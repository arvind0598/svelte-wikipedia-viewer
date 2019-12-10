<script>
  import SearchBox from './SearchBox.svelte';
  import ResultsBox from './ResultsBox.svelte';

  let searchTerm = '';
  let searchData = {
    status: 'INITIAL',
    results: [],
  };

  const fetchData = (event) => {
    console.log(searchTerm);
    searchData = {
      status: 'FETCHING',
      results: [],
    };

    fetch(`https://en.wikipedia.org/w/api.php?action=query&list=search&srsearch=${searchTerm}&format=json&origin=*`)
    .then(data => data.json())
    .then(data => {
      console.log(data.query.search);
      searchData = {
        status: 'FETCHED',
        results: data.query.search,
      };
    })
    .catch(err => {
      console.log(err);
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

.column--main {
  text-align: center;
}

* {
  font-family: 'Raleway', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  user-select: none;
}
</style>

<section class="hero is-fullheight is-primary is-bold">
  <div class="hero-body">
    <div class="container is-fluid">
      <div class="columns is-vcentered">
        <div class="column--main column is-4">
          <h1 class="title is-2"> Wikipedia Viewer </h1>
          <p class="subtitle is-4"> Search for an article, or get a random one <a href="https://en.wikipedia.org/wiki/Special:Random" target="_blank">here</a>.</p>
          <SearchBox bind:searchTerm={searchTerm} on:submit={fetchData}/>
        </div>
        <div class="column">
          <div class="container">
            <div class="columns is-multiline">
              <ResultsBox searchData={searchData}/>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>