<script>
  export let name;
  export let slug;
  export let src;
  export let href;
  export let title;

  $: cdn = slug ? `https://cdn.simpleicons.org/${slug}` : null;
  $: aria = title || name || 'icon';
  $: hasIcon = Boolean(src || slug);
</script>

<a
  class="icon-badge"
  class:has-icon={hasIcon}
  href={href}
  target={href ? "_blank" : undefined}
  rel={href ? "noopener noreferrer" : undefined}
  aria-label={aria}
>
  {#if hasIcon}
    <div class="icon-wrapper">
      {#if src}
        <img src={src} alt={name} />
      {:else if cdn}
        <img src={cdn} alt={name} />
      {/if}
    </div>
  {/if}
  <span class="label">{name}</span>
</a>

<style>
  .icon-badge {
    display: inline-flex;
    align-items: center;
    justify-content: flex-start;
    width: 260px;
    height: 56px;
    padding: 0.5rem 0.75rem;
    border-radius: 0.75rem;
    background: rgba(255, 255, 255, 0.02);
    border: 1px solid rgba(255, 255, 255, 0.08);
    text-decoration: none;
    color: inherit;
    transition: transform 0.15s ease, background 0.15s ease, border-color 0.15s ease;
    text-align: center;
  }

  .icon-badge:hover {
    transform: translateY(-2px);
    background: rgba(255, 255, 255, 0.06);
    border-color: rgba(255, 255, 255, 0.15);
  }

  /* When icon is present: left-align and keep spacing */
  .icon-badge.has-icon {
    justify-content: flex-start;
    text-align: left;
  }

  .icon-wrapper {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 32px;
    height: 32px;
    flex-shrink: 0;
    margin-right: 0.75rem;
  }

  .icon-wrapper img {
    width: 24px;
    height: 24px;
    object-fit: contain;
    filter: brightness(0) invert(1); /* bright white icons */
  }

  .label {
    font-size: 0.95rem;
    font-weight: 500;
    color: #e6edf3;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
</style>
