<script lang="ts">
  const socials = [
    { label: "GitHub",   href: "https://github.com/zoll-e"                                          },
    { label: "LinkedIn", href: "https://www.linkedin.com/in/zolt%C3%A1n-debreceni-56092a1b8/" },
    { label: "Email",    href: "mailto:debrecenizoltan19@gmail.com"         },
  ];
</script>

<footer style="
  background: #07000f;
  border-top: 1px solid rgba(255,0,255,0.1);
  padding: 2.5rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 1rem;
">
  <p style="font-size:0.7rem;color:rgba(255,255,255,0.2);letter-spacing:0.08em;">
    © {new Date().getFullYear()} Zoltan Debreceni
  </p>

  <div style="display:flex;gap:2rem;">
    {#each socials as s}
      <a href={s.href} target="_blank" rel="noopener noreferrer" style="
        font-size:0.72rem;letter-spacing:0.1em;text-transform:uppercase;
        color:rgba(255,255,255,0.3);text-decoration:none;font-weight:600;
        transition:color 0.2s,text-shadow 0.2s;
      "
        onmouseenter={(e) => {
          const t = e.currentTarget as HTMLElement;
          t.style.color = '#ff00ff';
          t.style.textShadow = '0 0 8px #ff00ff';
        }}
        onmouseleave={(e) => {
          const t = e.currentTarget as HTMLElement;
          t.style.color = 'rgba(255,255,255,0.3)';
          t.style.textShadow = 'none';
        }}
      >{s.label}</a>
    {/each}
  </div>

  <p style="font-size:0.65rem;color:rgba(255,0,255,0.3);letter-spacing:0.06em;font-style:italic;">
    Built with Svelte · Vim (still inside)
  </p>
</footer>
