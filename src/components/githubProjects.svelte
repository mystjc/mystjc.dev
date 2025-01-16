<script>
  const apis = [
    "https://api.github.com/repos/mystjc/dotfiles",
    "https://api.github.com/repos/mystjc/nixfiles",
    "https://api.github.com/repos/mystjc/zirconia",
    "https://api.github.com/repos/mystjc/mystjc.dev",
    "https://api.github.com/repos/mystjc/cobaltic"
  ];

  async function getRepos() {
    return await Promise.all(
      apis.map(async (api) => {
        const data = await fetch(api)
          .then(response => response.json()
        );
        return formatData(data);
      })
    );
  }

  function formatData(data) {
    return {
      url: data.html_url,
      avatar: data.owner.avatar_url,
      user: data.owner.login,
      name: data.name,
      desc: data.description,
      lang: data.language,
      stars: truncateCount(data.stargazers_count),
      forks: truncateCount(data.forks_count)
    }
  }

  function truncateCount(count) {
    return count >= 1000 ? `${(count / 1000).toFixed(0)}k` : count;
  }
</script>

{#await getRepos()}
  <p>Loading repos...</p>
{:then repos}
  {#each repos as repo}
    <div class="bg-gray-500 rounded-md p-4 m-4">
      <a href={repo.url} target="_blank">
        <div class="flex items-center">
          <img class="rounded-full w-6" src={repo.avatar.toString()} alt="">
          <span class="pl-2">{repo.user} / <strong>{repo.name}</strong></span>
        </div>
        <span>{repo.desc}</span>
        <div class="flex items-center">
          {#if repo.lang != null}
            <span class="pr-2">{repo.lang}</span>
          {/if}
          <img class="w-4" src="../../assets/icons/star.svg" alt="">
          <span class="px-1">{repo.stars}</span>
          <img class="w-4" src="../../assets/icons/repo-forked.svg" alt="">
          <span class="pl-1">{repo.forks}</span>
        </div>
      </a>
    </div>
  {/each}
{/await}
