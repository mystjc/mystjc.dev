<script>
  import { onMount } from 'svelte';
  let repos = null;

  onMount(async () => {
    const response = await fetch('https://api.github.com/users/mystjc/repos');
    const data = await response.json();
    repos = data;
  });
</script>

{#if repos}
  <ul class="text-white">
    {#each repos as repo}
      <li>
        <a href={repo.html_url} target="_blank">View on GitHub</a>
        <img src="{repo.owner.avatar_url}" alt="" width="10" height="10"> 
        <p>User: {repo.owner.login}</p>
        <p>Title: {repo.name}</p>
        <p>Description: {repo.description}</p>
        <p>Language: {repo.language}</p>
        <p>Stars: {repo.stargazers_count}</p>
      </li>
    {/each}
  </ul>
{:else}
  <p>Loading repos...</p>
{/if}
