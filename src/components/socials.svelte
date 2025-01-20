<script>
  const socials = new Map([
    ["Bluesky", {"url": "https://bsky.app/profile/mystjc.bsky.social", "svg": "../../logos/bluesky.svg"}],
    ["Mastodon", {"url": "https://mastodon.social/@mystjc", "svg": "../../logos/mastodon.svg"}],
    ["Spotify", {"url": "https://open.spotify.com/user/mystjcsonic", "svg": "../../logos/spotify.svg"}],
    ["Steam", {"url": "https://steamcommunity.com/id/mystjc/", "svg": "../../logos/steam.svg"}],
    ["Backloggd", {"url": "https://backloggd.com/u/Mystjc/", "svg": "../../logos/backloggd.svg"}],
    ["Trakt", {"url": "https://trakt.tv/users/mystjc", "svg": "../../logos/trakt.svg"}],
    ["Github", {"url": "https://github.com/mystjc", "svg": "../../logos/github.svg"}],
    ["Discord", {"url": "https://discordapp.com/users/334134328151769099", "svg": "../../logos/discord.svg"}]
  ]);
</script>

{#each [...socials] as [key, value]}
  <div class="bg-gray-500 rounded-md p-4 m-4">
    <a href={value.url} target="_blank">
      <div class="flex items-center">
        <img class="w-4" src={value.svg} alt="">
        <span class="pl-2">{key}</span>
      </div>
    </a>
  </div>
{/each}