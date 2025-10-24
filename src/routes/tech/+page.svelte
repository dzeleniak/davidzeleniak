<script>
  import Section from '$lib/components/Section.svelte';

  // ——— Languages ———
  const languages = [
    { name: 'Python', slug: 'python' },
    { name: 'Go', slug: 'go' },
    { name: 'Java', src: '/icons/Java.svg' },
    { name: 'C++', slug: 'cplusplus' },
    { name: 'C#', slug: 'dotnet' },
    { name: 'Rust', slug: 'rust' },
    { name: 'JavaScript', slug: 'javascript' },
    { name: 'TypeScript', slug: 'typescript' },
    { name: 'Bash', slug: 'gnubash' },
    { name: 'PowerShell', src: '/icons/Powershell.svg' },
    { name: 'Visual Basic', slug: 'dotnet' }
  ];

  // ——— Frameworks & Libraries ———
  const frameworks = [
    { name: 'FastAPI', slug: 'fastapi' },
    { name: 'Spring Boot', slug: 'springboot' },
    { name: '.NET', slug: 'dotnet' },
    { name: 'React', slug: 'react' },
    { name: 'React Native', slug: 'react' },
    { name: 'Next.js', slug: 'nextdotjs' },
    { name: 'Tailwind CSS', slug: 'tailwindcss' }
  ];

  // ——— Data Stores ———
  const dataStores = [
    { name: 'PostgreSQL', slug: 'postgresql' },
    { name: 'SQLite', slug: 'sqlite' },
    { name: 'MySQL', slug: 'mysql' },
    { name: 'MongoDB', slug: 'mongodb' },
    { name: 'Redis', slug: 'redis' },
    { name: 'InfluxDB', slug: 'influxdb' }
  ];

  // ——— Protocols & Messaging ———
  const protocolsMessaging = [
    { name: 'Kafka', slug: 'apachekafka' },
    { name: 'NATS', slug: 'natsdotio' },
    { name: 'RabbitMQ', slug: 'rabbitmq' },
    { name: 'gRPC' },
    { name: 'REST' }
  ];

  // ——— Platform & Cloud ———
  const platformCloud = [
    { name: 'Kubernetes', slug: 'kubernetes' },
    { name: 'Docker', slug: 'docker' },
    { name: 'AWS', src: '/icons/AWS.svg' },
    { name: 'Azure', src: '/icons/Azure.svg' },
    { name: 'Cloudflare', slug: 'cloudflare' }
  ];

  // ——— DevOps & IaC ———
  const devopsIac = [
    { name: 'Helm', slug: 'helm' },
    { name: 'Terraform', slug: 'terraform' },
    { name: 'GitLab CI/CD', slug: 'gitlab' },
    { name: 'Azure DevOps', src: '/icons/AzureDevops.svg' },
    { name: 'Prometheus', slug: 'prometheus' },
    { name: 'Grafana', slug: 'grafana' },
    { name: 'OpenTelemetry', slug: 'opentelemetry' }
  ];

  // ——— Build Tools ———
  const buildTools = [
    { name: 'CMake', slug: 'cmake' },
    { name: 'Poetry', slug: 'poetry' },
    { name: 'pip / PyPI', slug: 'pypi' },
    { name: 'UV', slug: 'uv' }
  ];

  // ——— Practices / Concepts ———
  const practices = [
    { name: 'Distributed Systems' },
    { name: 'Microservices Architecture' },
    { name: 'Event-Driven Architecture' },
    { name: 'Cloud-Native Design' },
    { name: 'CI/CD' },
    { name: 'Software Testing' },
    { name: 'Domain-Driven Design' },
    { name: 'Systems Architecture' }
  ];
</script>

<section class="container">
  <div class="page-header">
    <h1>Technology</h1>
    <p class="lede">
      A breakdown of the tools, languages, and practices I use to design distributed,
      reliable, and maintainable systems.
    </p>
  </div>

  <Section title="Languages" items={languages} />
  <Section title="Frameworks" items={frameworks} />
  <Section title="Data Stores" items={dataStores} />
  <Section title="Protocols & Messaging" items={protocolsMessaging} />
  <Section title="Platform & Cloud" items={platformCloud} />
  <Section title="DevOps & IaC" items={devopsIac} />
  <Section title="Build Tools" items={buildTools} />
  <Section title="Practices" items={practices} />
</section>

<style>
  /* remove redundant layout; handled globally */
  .page-header {
    margin-bottom: 2rem;
  }
</style>
