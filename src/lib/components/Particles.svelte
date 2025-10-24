<script>
  import { onMount } from 'svelte';

  // Tunables
  export let count = 40;          // number of particles (desktop)
  export let mobileCount = 24;    // fewer on mobile
  export let maxSpeed = 0.25;     // px per frame
  export let radiusMin = 0.6;     // px
  export let radiusMax = 1.9;     // px
  export let color = 'var(--accent-color)'; // uses your theme var

  let canvas, ctx, particles = [];
  let rafId;

  function initParticles(w, h, n) {
    const arr = [];
    for (let i = 0; i < n; i++) {
      arr.push({
        x: Math.random() * w,
        y: Math.random() * h,
        r: radiusMin + Math.random() * (radiusMax - radiusMin),
        dx: (Math.random() - 0.5) * maxSpeed,
        dy: (Math.random() - 0.5) * maxSpeed
      });
    }
    return arr;
  }

  function resize() {
    const dpr = Math.min(window.devicePixelRatio || 1, 2);
    canvas.width = Math.floor(innerWidth * dpr);
    canvas.height = Math.floor(innerHeight * dpr);
    canvas.style.width = '100%';
    canvas.style.height = '100%';
    ctx.setTransform(dpr, 0, 0, dpr, 0, 0);
  }

  function draw() {
    const { width: wCSS, height: hCSS } = canvas.getBoundingClientRect();
    ctx.clearRect(0, 0, wCSS, hCSS);

    // soft glow dots
    ctx.fillStyle = getComputedStyle(document.documentElement).getPropertyValue('--accent-color').trim() || '#759aff';
    ctx.globalAlpha = 0.45;

    for (const p of particles) {
      ctx.beginPath();
      ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
      ctx.fill();

      p.x += p.dx;
      p.y += p.dy;
      if (p.x < 0 || p.x > wCSS) p.dx *= -1;
      if (p.y < 0 || p.y > hCSS) p.dy *= -1;
    }

    rafId = requestAnimationFrame(draw);
  }

  onMount(() => {
    ctx = canvas.getContext('2d', { alpha: true });

    const prefersReduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
    const n = (innerWidth < 640 ? mobileCount : count);
    resize();
    particles = initParticles(innerWidth, innerHeight, prefersReduced ? 0 : n);

    const onResize = () => {
      resize();
      // keep current particles; they’ll bounce inside new bounds
    };
    const onVis = () => {
      if (document.hidden) cancelAnimationFrame(rafId);
      else rafId = requestAnimationFrame(draw);
    };

    window.addEventListener('resize', onResize);
    document.addEventListener('visibilitychange', onVis);

    if (!prefersReduced) rafId = requestAnimationFrame(draw);

    return () => {
      cancelAnimationFrame(rafId);
      window.removeEventListener('resize', onResize);
      document.removeEventListener('visibilitychange', onVis);
    };
  });
</script>

<canvas bind:this={canvas} class="bg-canvas" aria-hidden="true"></canvas>

<style>
  .bg-canvas {
    position: fixed;
    inset: 0;
    z-index: 0;           /* stays behind everything */
    pointer-events: none; /* never blocks clicks */
  }
</style>
