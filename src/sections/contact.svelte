<script lang="ts">
  import { onMount } from "svelte";
  import gsap from "gsap";
  import { ScrollTrigger } from "gsap/ScrollTrigger";

  gsap.registerPlugin(ScrollTrigger);

  let section: HTMLElement;

  onMount(() => {
    const els = section.querySelectorAll(".c-reveal");
    els.forEach((el, i) => {
      gsap.fromTo(el,
        { y: 40, opacity: 0 },
        {
          y: 0, opacity: 1, duration: 0.9, ease: "power3.out",
          delay: i * 0.1,
          scrollTrigger: { trigger: el, start: "top 85%" },
        }
      );
    });

    // magnetic email button
    const btn = section.querySelector<HTMLElement>(".mag-btn");
    if (btn) {
      btn.addEventListener("mousemove", (e) => {
        const r = btn.getBoundingClientRect();
        const dx = e.clientX - (r.left + r.width / 2);
        const dy = e.clientY - (r.top + r.height / 2);
        gsap.to(btn, { x: dx * 0.3, y: dy * 0.3, duration: 0.4, ease: "power2.out" });
      });
      btn.addEventListener("mouseleave", () => {
        gsap.to(btn, { x: 0, y: 0, duration: 0.7, ease: "elastic.out(1,0.5)" });
      });
    }
  });
</script>

<section
  bind:this={section}
  id="contact"
  class="contact-section"
  style="
    background: linear-gradient(155deg,#0e0008 0%,#180010 35%,#120009 65%,#080005 100%); padding: 7rem 2.5rem 5rem;
    position: relative; overflow: hidden;
    border-top: 1px solid rgba(255,0,255,0.08);
  "
>

  <!-- scanlines -->
  <div style="position:absolute;inset:0;pointer-events:none;background:repeating-linear-gradient(0deg,rgba(0,0,0,0.05) 0px,rgba(0,0,0,0.05) 1px,transparent 1px,transparent 3px);"></div>

  <!-- bg glow -->
  <div style="position:absolute;bottom:-10rem;left:50%;transform:translateX(-50%);width:40rem;height:20rem;background:radial-gradient(ellipse,rgba(255,0,255,0.08) 0%,transparent 70%);pointer-events:none;"></div>

  <div style="max-width:800px;margin:0 auto;text-align:center;position:relative;z-index:1;">
    <p class="c-reveal" style="font-size:0.65rem;letter-spacing:0.25em;text-transform:uppercase;color:#ff00ff88;font-weight:700;text-shadow:0 0 10px #ff00ff;margin-bottom:1.5rem;">
      Get in touch
    </p>

    <h2 class="c-reveal" style="
      font-size:clamp(3rem,8vw,7rem);font-weight:900;
      letter-spacing:-0.04em;line-height:0.92;
      color:#fff;margin-bottom:1.5rem;
      text-shadow:0 0 60px #ff00ff22;
    ">
      Let's build<br/>
      <span style="color:#ff00ff;text-shadow:0 0 30px #ff00ff;">something.</span>
    </h2>

    <p class="c-reveal" style="font-size:0.95rem;color:rgba(255,200,255,0.45);margin-bottom:3rem;line-height:1.6;">
      Got a project in mind? Looking for a fullstack engineer?<br/>Drop me a line — I reply fast.
    </p>

    <div class="c-reveal" style="display:flex;gap:1rem;justify-content:center;flex-wrap:wrap;">
      <a
        href="mailto:debrecenizoltan19@gmail.com"
        class="mag-btn"
        style="
          display:inline-flex;align-items:center;gap:0.5rem;
          background:#ff00ff;color:#0a0015;
          font-size:0.85rem;font-weight:800;letter-spacing:0.06em;
          padding:0.9rem 2.2rem;border-radius:3rem;text-decoration:none;
          box-shadow:0 0 30px #ff00ff44;
          transition:box-shadow 0.3s;
        "
        onmouseenter={(e) => (e.currentTarget as HTMLElement).style.boxShadow = '0 0 50px #ff00ff88'}
        onmouseleave={(e) => (e.currentTarget as HTMLElement).style.boxShadow = '0 0 30px #ff00ff44'}
      >
        Say hello →
      </a>

      <a href="https://www.linkedin.com/in/zolt%C3%A1n-debreceni-56092a1b8/" target="_blank" rel="noopener noreferrer" style="
        display:inline-flex;align-items:center;gap:0.5rem;
        border:1px solid rgba(255,0,255,0.35);color:#fff;
        font-size:0.85rem;font-weight:700;letter-spacing:0.06em;
        padding:0.9rem 2.2rem;border-radius:3rem;text-decoration:none;
        background:rgba(255,0,255,0.06);
        transition:all 0.3s;
      "
        onmouseenter={(e) => {
          const t = e.currentTarget as HTMLElement;
          t.style.borderColor = 'rgba(255,0,255,0.7)';
          t.style.background = 'rgba(255,0,255,0.12)';
        }}
        onmouseleave={(e) => {
          const t = e.currentTarget as HTMLElement;
          t.style.borderColor = 'rgba(255,0,255,0.35)';
          t.style.background = 'rgba(255,0,255,0.06)';
        }}
      >LinkedIn</a>
    </div>
  </div>
</section>

<style>
  @media (max-width: 768px) {
    .contact-section { padding: 4rem 1.5rem 3rem !important; }
  }
</style>
