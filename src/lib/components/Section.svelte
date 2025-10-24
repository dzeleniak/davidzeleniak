<script>
  import IconBadge from '$lib/components/IconBadge.svelte';
  export let title;
  export let items = [];
  export let bare = false;
</script>

<section class="block">
  {#if title}<h2>{title}</h2>{/if}

  <div class={bare ? 'list' : 'flex-wrap'}>
    {#each items as item}
      {#if bare}
        <div class="list-item">{item.name}</div>
      {:else}
        <IconBadge
          name={item.name}
          src={item.src}
          slug={item.slug}
          href={item.href}
          title={item.name}
        />
      {/if}
    {/each}
  </div>
</section>

<style>
  .block {
    margin: 1.75rem 0;
  }

  .block h2 {
    font-size: 1.35rem;
    margin: 0 0 1rem;
  }

  .flex-wrap {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem 1.25rem;
    justify-content: flex-start;
    align-items: flex-start;
  }

  @media (max-width: 640px) {
    .flex-wrap {
      justify-content: center;
    }
  }

  .list {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem 0.75rem;
  }

  .list-item {
    padding: 0.4rem 0.6rem;
    border: 1px dashed rgba(255, 255, 255, 0.15);
    border-radius: 0.6rem;
    color: #e6edf3;
    background: rgba(255, 255, 255, 0.03);
  }
</style>