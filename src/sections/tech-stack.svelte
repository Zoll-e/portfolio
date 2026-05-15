<script lang="ts">
  import { onMount } from "svelte";
  import gsap from "gsap";

  const row1 = [
    { icon: "devicon-html5-plain",                    name: "HTML"       },
    { icon: "devicon-css3-plain",                     name: "CSS"        },
    { icon: "devicon-typescript-plain",               name: "TypeScript" },
    { icon: "devicon-javascript-plain",               name: "JavaScript" },
    { icon: "devicon-react-original",                 name: "React"      },
    { icon: "devicon-nextjs-plain",                   name: "Next.js"    },
    { icon: "devicon-svelte-plain",                   name: "Svelte"     },
    { icon: "devicon-flutter-plain",                  name: "Flutter"    },
    { icon: "devicon-graphql-plain",                  name: "GraphQL"    },
    { icon: "devicon-vitejs-plain",                   name: "Vite"       },
    { icon: "devicon-tailwindcss-plain",              name: "Tailwind"   },
    { icon: "devicon-playwright-plain",               name: "Playwright" },
  ];

  const row2 = [
    { icon: "devicon-nodejs-plain",                        name: "Node.js"    },
    { icon: "devicon-express-original",                    name: "Express"    },
    { icon: "devicon-docker-plain",                        name: "Docker"     },
    { icon: "devicon-kubernetes-plain",                    name: "K8s"        },
    { icon: "devicon-postgresql-plain",                    name: "PostgreSQL" },
    { icon: "devicon-mongodb-plain",                       name: "MongoDB"    },
    { icon: "devicon-mysql-plain",                         name: "MySQL"      },
    { icon: "devicon-redis-plain",                         name: "Redis"      },
    { icon: "devicon-nginx-original",                      name: "Nginx"      },
    { icon: "devicon-git-plain",                           name: "Git"        },
    { icon: "devicon-github-original",                     name: "GitHub"     },
    { icon: "devicon-amazonwebservices-plain-wordmark",    name: "AWS"        },
    { icon: "devicon-googlecloud-plain",                   name: "GCP"        },
    { icon: "devicon-firebase-plain",                      name: "Firebase"   },
    { icon: "devicon-vercel-original",                     name: "Vercel"     },
    { icon: "devicon-bash-plain",                          name: "Bash"       },
    { icon: "devicon-vim-plain",                           name: "Vim btw"    },
  ];

  let track1: HTMLElement;
  let track2: HTMLElement;

  onMount(() => {
    const isMobile = window.innerWidth < 768;
    const duration = isMobile ? 20 : 40;

    gsap.to(track1, { x: "-50%", duration, ease: "none", repeat: -1 });
    gsap.to(track2, { x: "0%", duration, ease: "none", repeat: -1, startAt: { x: "-50%" } });
  });
</script>

<section id="stack" style="padding:1.5rem 0;overflow:hidden;position:relative;background:#000;border-top:1px solid rgba(255,255,255,0.06);border-bottom:1px solid rgba(255,255,255,0.06);">
  <div style="display:flex;align-items:center;gap:2rem;padding:0 2rem;margin-bottom:1rem;">
    <p style="font-size:0.6rem;letter-spacing:0.2em;text-transform:uppercase;color:rgba(255,255,255,0.2);font-weight:700;white-space:nowrap;flex-shrink:0;">Tech stack</p>
    <div style="flex:1;height:1px;background:rgba(255,255,255,0.06);"></div>
  </div>

  <div style="display:flex;flex-direction:column;gap:0.75rem;">
    <div style="overflow:hidden;position:relative;">
      <div style="position:absolute;top:0;bottom:0;left:0;width:4rem;background:linear-gradient(to right,#000,transparent);z-index:10;pointer-events:none;"></div>
      <div style="position:absolute;top:0;bottom:0;right:0;width:4rem;background:linear-gradient(to left,#000,transparent);z-index:10;pointer-events:none;"></div>
      <div bind:this={track1} style="display:flex;gap:2rem;white-space:nowrap;will-change:transform;align-items:center;padding:0.2rem 0;">
        {#each [...row1, ...row1] as tech}
          <div role="img" aria-label={tech.name}
            style="display:inline-flex;flex-direction:column;align-items:center;gap:0.25rem;flex-shrink:0;opacity:0.4;transition:opacity 0.25s;"
            onmouseenter={(e) => (e.currentTarget as HTMLElement).style.opacity = '1'}
            onmouseleave={(e) => (e.currentTarget as HTMLElement).style.opacity = '0.4'}
          >
            <i class={tech.icon} style="font-size:1.3rem;color:#fff;"></i>
            <span style="font-size:0.5rem;color:rgba(255,255,255,0.35);letter-spacing:0.07em;font-weight:600;text-transform:uppercase;">{tech.name}</span>
          </div>
        {/each}
      </div>
    </div>

    <div style="overflow:hidden;position:relative;">
      <div style="position:absolute;top:0;bottom:0;left:0;width:4rem;background:linear-gradient(to right,#000,transparent);z-index:10;pointer-events:none;"></div>
      <div style="position:absolute;top:0;bottom:0;right:0;width:4rem;background:linear-gradient(to left,#000,transparent);z-index:10;pointer-events:none;"></div>
      <div bind:this={track2} style="display:flex;gap:2rem;white-space:nowrap;will-change:transform;align-items:center;padding:0.2rem 0;">
        {#each [...row2, ...row2] as tech}
          <div role="img" aria-label={tech.name}
            style="display:inline-flex;flex-direction:column;align-items:center;gap:0.25rem;flex-shrink:0;opacity:0.4;transition:opacity 0.25s;"
            onmouseenter={(e) => (e.currentTarget as HTMLElement).style.opacity = '1'}
            onmouseleave={(e) => (e.currentTarget as HTMLElement).style.opacity = '0.4'}
          >
            <i class={tech.icon} style="font-size:1.3rem;color:#fff;"></i>
            <span style="font-size:0.5rem;color:rgba(255,255,255,0.35);letter-spacing:0.07em;font-weight:600;text-transform:uppercase;">{tech.name}</span>
          </div>
        {/each}
      </div>
    </div>
  </div>
</section>
