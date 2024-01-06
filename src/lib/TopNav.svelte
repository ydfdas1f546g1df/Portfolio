<script lang="ts">
    export let links: {
        name: string,
        url: string,
    }[] = []

</script>

<style lang="less">
  @import "$lib/colors";

  .TopNav {
    background-color: lighten(@backgroundcolor, 15%);
    ul{
      display: flex;
      justify-content: center;
      list-style: none;
      padding: 0;
      margin: 0;
      padding-top: 0.8rem;
      padding-bottom: 0.8rem;
      height: auto;
      li{
        margin-left: 1rem;
        margin-right: 1rem;
      }
    }
  }
</style>

<div class="TopNav">
    <ul>
        {#each links as link}
            <li>
                <a href={link.url}>{link.name}</a>
            </li>
        {/each}
    </ul>
</div>