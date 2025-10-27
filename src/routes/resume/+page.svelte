<script>
  const roles = [
    {
      company: 'EO Solutions',
      title: 'Software Engineer',
      period: 'Jan 2024 — Present',
      logo: '/logos/eosolutions.jpg',
      bullets: [
        'Distributed control software in Python/C++ for HWIL & HPC systems',
        'Distributed intelligence platform for reliability/throughput/fault tolerance',
        'APIs & microservices (FastAPI, Spring Boot) for real-time data flows',
        'C&DH architecture: hardware I/O, messaging middleware, telemetry pipelines',
        'Kubernetes + Helm deployments for automated test & on-prem control',
        'Modular, plugin-based C2 engine for multi-sensor integration'
      ],
      tech: ['Python', 'C++', 'FastAPI', 'Asyncio', 'NATS', 'gRPC', 'Kubernetes', 'Helm', 'Docker', 'GitLab CI/CD', 'Spring Boot']
    },
    {
      company: 'Kimberly-Clark',
      title: 'Full-Stack Engineer',
      period: 'Jul 2023 — Jan 2024',
      logo: '/logos/kimberlyclark.png',
      bullets: [
        'Internal ChatGPT client (Next.js, Tailwind, Azure Cognitive Services)',
        'Azure DevOps CI/CD for internal web apps',
        'Huggies web sizing tool (projected >$10M annual impact)',
        'Multi-tenant microservice architecture in Azure'
      ],
      tech: ['Next.js', 'TypeScript', 'Tailwind CSS', 'Azure', 'Terraform', 'Cosmos DB', 'Azure DevOps']
    },
    {
      company: 'Kimberly-Clark',
      title: 'Cloud Automation Engineer',
      period: 'May 2022 — Jul 2023',
      logo: '/logos/kimberlyclark.png',
      bullets: [
        'Global site management platform (ASP.NET, Blazor)',
        'Azure Key Vault rotation pipelines',
        'Terraform modules & CI/CD templates (org-wide)',
        'AKS + Helm deployment pipelines'
      ],
      tech: ['Azure', 'Terraform', 'Azure DevOps', '.NET (C#, VB)', 'Kubernetes', 'Cloudflare']
    },
    {
      company: 'Cloudsurf Software',
      title: 'Software Developer',
      period: 'Jan 2020 — Jan 2021',
      logo: '/logos/eosolutions.jpg',
      bullets: ['React & React Native apps integrated with AWS Lambda'],
      tech: ['React', 'React Native', 'AWS Lambda', 'JavaScript']
    },
    {
      company: 'C-Los Design Solutions',
      title: 'BIM Engineer',
      period: 'May 2019 — May 2022',
      logo: '/logos/cds.jpg',
      bullets: ['.NET & Autodesk SDK tools; cross-discipline coordination on $500M project'],
      tech: ['Autodesk Revit', 'Navisworks', 'AutoCAD', '.NET (C#)']
    },
    {
      company: 'University of Nevada, Las Vegas',
      title: 'Software Development Intern',
      period: 'Aug 2018 — May 2019',
      logo: '/logos/unlv.png',
      bullets: ['ASP.NET & Java Spring apps for identity/portal systems'],
      tech: ['ASP.NET', 'Java Spring', 'OracleDB']
    },
    {
      company: 'Southland Industries',
      title: 'Information Technology Intern',
      period: 'May 2017 — Aug 2018',
      logo: '/logos/southland.jpg',
      bullets: ['On-site support & sysadmin in Windows Server environments'],
      tech: ['Windows Server', 'PowerShell', 'Active Directory']
    }
  ];
</script>

<section class="container">
  <div class="page-header">
    <h1>Resume</h1>
    <p class="lede">A quick timeline of my recent work history and impact.</p>
  </div>

  <div class="timeline">
    {#each roles as r}
      <article class="item">
        <div class="dot" aria-hidden="true"></div>
        <details class="content">
          <summary>
            <div class="header">
              {#if r.logo}
                <span class="logo-mask" style="--logo: url({r.logo})" aria-hidden="true"></span>
                <img class="logo-fallback" src={r.logo} alt="" aria-hidden="true" />
              {/if}
              <h3>{r.company}</h3>
              <div class="meta">
                <span class="role">{r.title}</span>
                <span class="sep">•</span>
                <time>{r.period}</time>
              </div>
            </div>
          </summary>

          <ul class="bullets">
            {#each r.bullets as b}
              <li>{b}</li>
            {/each}
          </ul>

          {#if r.tech?.length}
            <div class="tech">
              {#each r.tech as t}
                <span class="chip">{t}</span>
              {/each}
            </div>
          {/if}

          <!-- show the period/date as part of the expanded content -->
          <div class="open-meta">
            <time>{r.period}</time>
          </div>
        </details>
      </article>
    {/each}
  </div>
</section>

<style>
  /* Layout already provided by app.css (container, h1, lede, .chip) */

  /* Timeline */
  .timeline {
    position: relative;
    margin-top: 1rem;
    padding-left: 1.25rem;
  }

  .timeline::before {
    content: "";
    position: absolute;
    left: .375rem;
    top: .25rem;
    bottom: .25rem;
    width: 2px;
    background: linear-gradient(to bottom, rgba(255,255,255,.25), rgba(255,255,255,.08));
  }

  .item {
    position: relative;
    display: grid;
    grid-template-columns: 1.25rem 1fr;
    gap: .75rem;
    padding: .5rem 0 1.25rem;
  }

  .dot {
    grid-column: 1;
    width: .75rem;
    height: .75rem;
    border-radius: 999px;
    background: var(--accent-color);
    box-shadow: 0 0 0 3px rgba(117,154,255,.15);
    margin-top: .55rem;
  }

  details.content {
    grid-column: 2;
    border: 1px solid var(--border-color);
    border-radius: .9rem;
    background: var(--surface);
    transition: border-color .15s ease, background .15s ease;
  }

  details[open] {
    border-color: var(--border-color-strong);
    background: var(--surface-hover);
  }

  summary {
    cursor: pointer;
    list-style: none;
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    padding: .85rem 1rem;
    user-select: none;
  }

  summary::-webkit-details-marker {
    display: none;
  }

  summary::after {
    content: "▾";
    transition: transform .2s ease;
  }

  details[open] summary::after {
    transform: rotate(180deg);
  }

  .header {
    display: flex;
    align-items: center;
    gap: .6rem;
  }

  .header h3 {
    font-size: 1.1rem;
    margin: 0;
  }

  .meta {
    display: flex;
    gap: .5rem;
    font-size: .92rem;
    color: #9aa4b2;
  }

  /* hide the date/period and separator in the compact summary to reduce horizontal width */
  .meta time,
  .meta .sep {
    display: none;
  }

  /* when expanded, show a dedicated date block inside the content */
  .open-meta { display: none; }
  details[open] .open-meta { display: block; color: var(--muted-color); font-size: .95rem; margin: 0 1rem 1rem 1rem; }

  .role { color: var(--text-color); }

  .bullets {
    margin: .5rem 0 0;
    padding: 0 1rem 1rem 2rem;
    line-height: 1.6;
    color: var(--muted-color);
  }

  .bullets li { margin: .25rem 0; }

  .tech {
    display: flex;
    flex-wrap: wrap;
    gap: .4rem .6rem;
    margin: 0 1rem 1rem 1rem;
  }

  /* Logo masks */
  .logo-mask {
    width: 32px;
    height: 32px;
    background: #fff;
    -webkit-mask-image: var(--logo);
    mask-image: var(--logo);
    -webkit-mask-size: contain;
    mask-size: contain;
    -webkit-mask-repeat: no-repeat;
    mask-repeat: no-repeat;
    -webkit-mask-position: center;
    mask-position: center;
    mask-mode: luminance;
  }

  .logo-fallback {
    width: 22px;
    height: 22px;
    object-fit: contain;
    display: none;
    filter: brightness(0) invert(1) saturate(0) contrast(180%);
  }

  @supports not ((mask-image: url("")) or (-webkit-mask-image: url(""))) {
    .logo-mask { display: none; }
    .logo-fallback { display: inline-block; }
  }

  details.content:not([open]) .logo-mask,
  details.content:not([open]) .logo-fallback {
    opacity: .9;
  }

  @media (max-width: 520px) {
    .timeline::before { left: .33rem; }
    .item { grid-template-columns: 1rem 1fr; }
    .dot { width: .6rem; height: .6rem; margin-top: .6rem; }
    /* slightly smaller company names on mobile */
    .header h3 { font-size: 1rem; }

    /* hide company name on mobile in collapsed state to save horizontal space;
       show it when the card is expanded (details[open]) so users can still see full info */
    .header h3 { display: none; }
    details[open] .header h3 { display: block; }
  }
</style>
