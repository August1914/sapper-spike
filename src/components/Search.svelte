<script>
    export let repositories;
    let userSearchTerm = "";
    $: filteredRepos = repositories.filter((repo) => {
        return repo.name.toLowerCase().includes(userSearchTerm.toLowerCase())
    });

    function filter(repositories, userSearchTerm) {
        return repositories.filter((repo) => {
            return repo.name.toLowerCase().includes(userSearchTerm.toLowerCase());
        });
    }
    $: console.log(userSearchTerm)
</script>

<style>
  .search-wrapper {
      border: 1px solid #ccc;
      border-radius: 10px;
      padding: 5px;
      margin: 10px auto;
  }

  .search-form input {
      border-top-left-radius: 10px;
      border-top-right-radius: 10px;
      width: 100%;
  }
  ul {
      list-style: none;
      margin: 0;
      padding: 0;
  }
  li {
      padding: 10px 5px;
  }

  li:nth-child(odd) {
      background-color: lightblue;
  }
  code {
      display: block;
  }
</style>

<div class="search-wrapper">
    <form class="search-form">
        <input type="text" bind:value={userSearchTerm} placeholder="search for repositories"/>
    </form>
<p>Search component</p>
{#each filter(repositories, userSearchTerm) as repository}
<li><strong>{repository.name}</strong><code>{repository.url}</code></li>
{/each}
</div>
