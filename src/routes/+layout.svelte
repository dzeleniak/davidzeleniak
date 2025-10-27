<script>
  import "../app.css"
  import Particles from '$lib/components/Particles.svelte';
  import { page } from '$app/stores';

  // mobile menu state
  let menuOpen = false;

  const pages = [
    { title: 'Home', href: '/' },
    { title: 'About', href: '/about' },
    { title: 'Technology', href: '/tech' },
    { title: 'Resume', href: '/resume' }
  ];

  const socials = [
    { name: 'LinkedIn', href: 'https://www.linkedin.com/in/dzeleniak/', icon: '/logos/linkedin.svg' },
    { name: 'Email', href: 'mailto:zeleniak.david@gmail.com', icon: '/icons/mail.svg' }
  ];
</script>

<svelte:head>
  <title>David Zeleniak</title>
  <link rel="icon" href="/favicon.ico" sizes="any" />
  <link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png" />
  <link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png" />
  <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png" />
  <link rel="manifest" href="/site.webmanifest" />
  <link rel="shortcut icon" href="/favicon.ico" />
  <meta name="theme-color" content="#0f0f0f" />
  <meta name="apple-mobile-web-app-title" content="David Zeleniak" />
  <meta name="application-name" content="David Zeleniak" />
</svelte:head>

<Particles count={40} mobileCount={22} maxSpeed={0.25} />

<header class="site-header" class:open={menuOpen}>
  <div class="header-left">
    <!-- desktop caret that indicates the menu; clicking toggles the menu open state -->
    <button
      class="menu-caret"
      aria-label="Toggle menu"
      aria-expanded={menuOpen}
      on:click={() => (menuOpen = !menuOpen)}
    >
      <svg width="18" height="18" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
        <!-- right-pointing caret -->
        <path d="M8 5l8 7-8 7" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
      </svg>
    </button>
    <!-- mobile toggle (left-aligned caret) — shown on mobile; replaces the hamburger visually -->
    <button
      class="mobile-toggle"
      on:click={() => (menuOpen = !menuOpen)}
      aria-expanded={menuOpen}
      aria-label="Toggle menu"
    >
      <svg width="18" height="18" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
        <path d="M8 5l8 7-8 7" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
      </svg>
    </button>

    <!-- desktop nav (visible on larger screens) -->
    <nav class="site-nav">
      {#each pages as p}
        <a
          href={p.href}
          class="nav-link header-nav-link"
          aria-current={$page.url.pathname === p.href ? 'page' : undefined}
          class:active={$page.url.pathname === p.href}
        >
          {p.title}
        </a>
      {/each}
    </nav>
  </div>

  <!-- old mobile toggle removed from here; caret button is now inside header-left and used on mobile -->

  <!-- right area: socials + mobile nav (shown when menuOpen on small screens) -->
  <div class="site-header__right">
    {#each socials as s}
      <a
        class="site-header__icon"
        href={s.href}
        target="_blank"
        rel="noopener noreferrer"
        aria-label={s.name}
      >
        <img src={s.icon} alt={s.name} />
      </a>
    {/each}
  </div>

  </header>

{#if menuOpen}
  <div class="mobile-dropdown" role="menu">
    {#each pages as p}
      <a
        href={p.href}
        class="nav-link mobile-nav-link"
        role="menuitem"
        on:click={() => (menuOpen = false)}
      >
        {p.title}
      </a>
    {/each}
  </div>
{/if}

<main class="container">
  <slot />
</main>

<style>
  .site-header {
    width: 100%;
    position: fixed;
    top: 0;
    left: 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    /* include safe-area insets on left/right so icons don't get pushed off-screen */
    box-sizing: border-box;
    padding: calc(0.75rem + env(safe-area-inset-top)) calc(1.25rem + env(safe-area-inset-right)) 0.9rem calc(1.25rem + env(safe-area-inset-left));
    background: rgba(13, 17, 23, 0.85);
    backdrop-filter: blur(6px);
    z-index: 60;
    overflow: hidden; /* prevent horizontal overflow beyond the viewport */
  }

  .header-left {
    display: flex;
    align-items: center;
  }

  .home-icon {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 28px;
    height: 28px;
    transition: transform 0.15s ease, opacity 0.15s ease;
  }

  .home-icon img {
    width: 22px;
    height: 22px;
    filter: grayscale(1) brightness(0.8) contrast(2.05) invert(1);
    mix-blend-mode: screen;
    opacity: 0.9;
    transition: opacity 0.15s ease, transform 0.15s ease;
  }

  .home-icon:hover img {
    opacity: 1;
  }

  .menu-caret {
    display: none; /* shown on desktop via media query */
    background: transparent;
    border: 0;
    color: var(--text-color);
    padding: 0.25rem;
    align-items: center;
    justify-content: center;
  }

  .menu-caret svg {
    transition: transform 160ms ease-in-out;
    transform: rotate(0deg);
  }

  /* rotate caret when header is hovered or when menu is open */
  .site-header:hover .menu-caret svg,
  .site-header.open .menu-caret svg {
    transform: rotate(90deg);
  }

  .site-header__right {
    display: flex;
    align-items: center;
    gap: 1rem;
    /* keep some extra breathing room on the right so icons aren't flush to the viewport */
    padding-right: calc(0.5rem + env(safe-area-inset-right));
  }

  /* mobile-caret behaves similarly to desktop caret (rotates when open) */
  .mobile-toggle {
    display: none; /* shown on mobile via media query; placed on left in DOM */
    background: transparent;
    border: 0;
    color: var(--text-color);
    padding: 0.25rem;
    align-items: center;
    justify-content: center;
  }

  .mobile-toggle svg {
    transition: transform 160ms ease-in-out;
    transform: rotate(0deg);
  }

  .site-header.open .mobile-toggle svg {
    transform: rotate(90deg);
  }

  .site-nav {
    display: flex;
    gap: 0.75rem;
    margin-left: 1rem;
    align-items: center;
  }

  /* On desktop we keep the nav hidden until the header is hovered or focused (keyboard access) */
  @media (min-width: 821px) {
    .site-nav {
      opacity: 0;
      transform: translateY(-6px);
      pointer-events: none;
      /* don't toggle visibility immediately — rely on opacity/transform for smooth transitions */
      transition: opacity 160ms ease-in-out, transform 160ms ease-in-out;
    }

    .site-header:hover .site-nav,
    .site-nav:focus-within {
      opacity: 1;
      transform: translateY(0);
      pointer-events: auto;
    }

    /* also reveal when menuOpen toggled via the caret */
    .site-header.open .site-nav {
      opacity: 1;
      transform: translateY(0);
      pointer-events: auto;
    }
  }

  .header-nav-link {
    padding: 0.35rem 0.6rem;
    border-radius: 0.5rem;
  }

  .header-nav-link.active,
  .header-nav-link[aria-current="page"] {
    background: rgba(117,154,255,0.12);
    color: var(--accent-color);
    border: 1px solid rgba(117,154,255,0.18);
  }

  .site-header__icon {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 0.15rem;
  }

  .site-header__icon img {
    display: block;
    width: 22px;
    height: 22px;
    max-width: 100%;
    object-fit: contain;
    filter: grayscale(1) brightness(0.8) contrast(2.05) invert(1);
    mix-blend-mode: screen;
    opacity: 0.9;
    transition: opacity 0.15s ease, transform 0.15s ease;
  }

  .site-header__icon:hover img {
    opacity: 1;
    transform: scale(1.1);
    filter: brightness(1.3) saturate(1.4);
  }

  main.container {
    position: relative;
    z-index: 1;
    margin-top: 12vh;
    padding: 0 1.5rem;
  }

  /* mobile-specific styling */
  .mobile-toggle {
    display: none;
    background: transparent;
    border: 0;
    color: var(--text-color);
    padding: 0.25rem;
    align-self: center;
  }

  .mobile-dropdown {
    position: fixed;
    left: 0;
    right: 0;
    /* place dropdown under the header; use safe-area inset so it clears notches */
    top: calc(env(safe-area-inset-top) + 3.2rem);
    background: rgba(10,12,14,0.92);
    backdrop-filter: blur(6px);
    padding: 0.75rem 1rem 1rem 1rem;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    z-index: 120;
    color: var(--text-color);
    box-shadow: 0 8px 24px rgba(0,0,0,0.6);
  }

  .mobile-nav-link { padding: 0.6rem 0.75rem; border-radius: 0.5rem; color: var(--text-color); }

  /* ensure general nav links are readable on all backgrounds */
  .nav-link { color: var(--text-color); }

  @media (max-width: 820px) {
    .site-nav { display: none; }
    /* show the mobile caret on mobile and hide the desktop caret */
    .mobile-toggle { display: inline-flex; }
    .menu-caret { display: none; }

    .site-header__right { gap: 0.6rem; }
  }

  @media (max-width: 420px) {
    main.container { margin-top: 9vh; }
  }

  /* show the desktop caret on wider screens */
  @media (min-width: 821px) {
    .menu-caret { display: inline-flex; }
  }
</style>
