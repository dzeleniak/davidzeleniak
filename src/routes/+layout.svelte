<script>
  import "../app.css"
  import Particles from '$lib/components/Particles.svelte';
  import { page } from '$app/stores';

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

<header class="site-header">
  <div class="header-left">
    <a href="/" class="home-icon" aria-label="Home">
      <img src="/icons/house.svg" alt="Home" />
    </a>
  </div>

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
    padding: 1.25rem 1.5rem;
    background: rgba(13, 17, 23, 0.65);
    backdrop-filter: blur(6px);
    z-index: 10;
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

  .site-header__right {
    display: flex;
    align-items: center;
    gap: 1rem;
  }

  .site-header__icon img {
    width: 22px;
    height: 22px;
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

  @media (max-width: 640px) {
    .site-header {
      flex-direction: column;
      justify-content: center;
      gap: 0.75rem;
    }
  }
</style>
