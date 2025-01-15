<script>
  import { onMount } from 'svelte';
  
  let repos = [];
  let hasFetchedRepos = false;
  const apiLinks = [
    "https://api.github.com/repos/mystjc/dotfiles",
    "https://api.github.com/repos/mystjc/nixfiles",
    "https://api.github.com/repos/mystjc/zirconia",
    "https://api.github.com/repos/mystjc/mystjc.dev",
    "https://api.github.com/repos/mystjc/cobaltic"
  ]
  
  onMount (async () => {
    await getRepos();
  });

  async function getRepos() {
    for (let link of apiLinks) {
      const data = await fetch(link).then(
        (response) => response.json()
      );
      repos.push(data);
    }
    hasFetchedRepos = true;
  }
</script>

{#if hasFetchedRepos}
  {#each repos as repo}
    <div class="bg-gray-500 rounded-md p-4 m-4">
      <a href={repo.html_url} target="_blank">
        <div class="flex items-center">
          <img class="rounded-full w-6" src={repo.owner.avatar_url.toString()} alt="">
          <span class="pl-2">{repo.owner.login} / <strong>{repo.name}</strong></span>
        </div>
        <span>{repo.description}</span>
        <div class="flex items-center">
          {#if repo.language != null}
            <span class="pr-2">{repo.language}</span>
          {/if}
          <img class="w-4" src="../../assets/icons/star-regular.svg" alt="">
          <span class="pl-1">{repo.stargazers_count}</span>
        </div>
      </a>
    </div>
  {/each}
{:else}
  <p>Loading repos...</p>
{/if}
