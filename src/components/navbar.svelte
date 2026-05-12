<script lang="ts">
  import { onMount } from "svelte";
  import gsap from "gsap";

  let nav: HTMLElement;
  let scrolled = false;

  const links = [
    { label: "About",    href: "#about"    },
    { label: "Projects", href: "#projects" },
    { label: "Stack",    href: "#stack"    },
    { label: "Contact",  href: "#contact"  },
  ];

  onMount(() => {
    gsap.fromTo(nav,
      { y: -60, opacity: 0 },
      { y: 0, opacity: 1, duration: 0.8, ease: "power3.out", delay: 1.6 }
    );

    const onScroll = () => { scrolled = window.scrollY > 60; };
    window.addEventListener("scroll", onScroll);
    return () => window.removeEventListener("scroll", onScroll);
  });
</script>

<nav
  bind:this={nav}
  style="
    position: fixed; top: 0; left: 0; right: 0; z-index: 500;
    display: flex; align-items: center; justify-content: space-between;
    padding: 1.1rem 2.5rem;
    transition: background 0.4s, backdrop-filter 0.4s, border-color 0.4s;
    background: {scrolled ? 'rgba(10,0,21,0.85)' : 'transparent'};
    backdrop-filter: {scrolled ? 'blur(14px)' : 'none'};
    border-bottom: 1px solid {scrolled ? 'rgba(255,0,255,0.12)' : 'transparent'};
  "
>
  <a href="#header" style="
    font-size: 0.9rem; font-weight: 900; letter-spacing: 0.08em;
    color: #fff; text-decoration: none;
    text-shadow: 0 0 20px #ff00ff44;
  ">ZD<span style="color:#ff00ff;">.</span></a>

  <ul class="nav-links" style="display:flex;gap:2.5rem;list-style:none;margin:0;padding:0;">
    {#each links as l}
      <li>
        <a href={l.href} style="
          font-size: 0.75rem; letter-spacing: 0.1em; text-transform: uppercase;
          color: rgba(255,255,255,0.45); text-decoration: none; font-weight: 600;
          transition: color 0.2s, text-shadow 0.2s;
        "
          onmouseenter={(e) => {
            const t = e.currentTarget as HTMLElement;
            t.style.color = '#fff';
            t.style.textShadow = '0 0 10px #ff00ff88';
          }}
          onmouseleave={(e) => {
            const t = e.currentTarget as HTMLElement;
            t.style.color = 'rgba(255,255,255,0.45)';
            t.style.textShadow = 'none';
          }}
        >{l.label}</a>
      </li>
    {/each}
  </ul>

  <a href="mailto:debrecenizoltan19@gmail.com" style="
    font-size: 0.72rem; letter-spacing: 0.1em; text-transform: uppercase;
    color: #ff00ff; text-decoration: none; font-weight: 700;
    border: 1px solid #ff00ff55; padding: 0.4rem 1rem; border-radius: 2rem;
    background: rgba(255,0,255,0.06);
    transition: all 0.25s;
    text-shadow: 0 0 8px #ff00ff;
    box-shadow: 0 0 12px #ff00ff11;
  "
    onmouseenter={(e) => {
      const t = e.currentTarget as HTMLElement;
      t.style.background = 'rgba(255,0,255,0.15)';
      t.style.boxShadow = '0 0 20px #ff00ff33';
    }}
    onmouseleave={(e) => {
      const t = e.currentTarget as HTMLElement;
      t.style.background = 'rgba(255,0,255,0.06)';
      t.style.boxShadow = '0 0 12px #ff00ff11';
    }}
  >Hire me</a>
</nav>

<style>
  @media (max-width: 768px) {
    .nav-links { display: none !important; }
  }
</style>
