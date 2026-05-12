<script lang="ts">
  import { onMount } from "svelte";
  import gsap from "gsap";
  import { ScrollTrigger } from "gsap/ScrollTrigger";
  gsap.registerPlugin(ScrollTrigger);

  let section: HTMLElement;
  onMount(() => {
    section.querySelectorAll(".a-reveal").forEach((el, i) => {
      gsap.fromTo(el, { y:40,opacity:0 }, {
        y:0,opacity:1,duration:0.8,ease:"power3.out",delay:i*0.09,
        scrollTrigger:{ trigger:el, start:"top 88%" },
      });
    });
  });

  const facts = [
    { val:"3+", label:"Years building products" },
    { val:"10+",label:"Technologies shipped"    },
    { val:"∞",  label:"Vim escape attempts"     },
  ];
</script>

<section bind:this={section} id="about" class="about-section" style="
  background:#000; padding:7rem 2.5rem;
  position:relative; overflow:hidden;
  border-top:1px solid rgba(255,0,255,0.08);
">

  <div class="about-grid" style="max-width:1100px;margin:0 auto;position:relative;z-index:1;display:grid;grid-template-columns:1fr 1fr;gap:5rem;align-items:start;">
    <div>
      <p class="a-reveal" style="font-size:0.65rem;letter-spacing:0.25em;text-transform:uppercase;color:#ff00ff;font-weight:700;text-shadow:0 0 12px #ff00ff;margin-bottom:1rem;">About</p>
      <h2 class="a-reveal" style="font-size:clamp(2rem,4vw,3.2rem);font-weight:900;color:#fff;letter-spacing:-0.03em;line-height:1.05;margin-bottom:2rem;text-shadow:0 0 40px #ff00ff22;">
        Fullstack engineer<br/>who ships.
      </h2>
      <div style="display:flex;flex-direction:column;gap:1rem;">
        <p class="a-reveal" style="font-size:0.95rem;color:rgba(255,200,255,0.55);line-height:1.75;">
          I build end-to-end products — pixel-perfect mobile UIs in React Native and Flutter backed by GCP and AWS. I care about the full picture, not just my slice.
        </p>
        <p class="a-reveal" style="font-size:0.95rem;color:rgba(255,200,255,0.55);line-height:1.75;">
          Sweet spot: mobile-first apps with Firebase or serverless GCP. Fast to ship, easy to scale.
        </p>
        <p class="a-reveal" style="font-size:0.95rem;color:#ff00ff;line-height:1.75;font-style:italic;text-shadow:0 0 10px #ff00ff44;">
          Also: I use Neovim. The exit key is a myth.
        </p>
      </div>
    </div>

    <div style="display:flex;flex-direction:column;gap:1rem;padding-top:3rem;">
      {#each facts as f}
        <div class="a-reveal" style="padding:1.5rem 2rem;border:1px solid rgba(255,0,255,0.2);border-radius:0.75rem;background:rgba(255,0,255,0.05);display:flex;align-items:center;gap:1.5rem;">
          <span style="font-size:2.5rem;font-weight:900;color:#ff00ff;letter-spacing:-0.04em;text-shadow:0 0 20px #ff00ff;min-width:3.5rem;">{f.val}</span>
          <span style="font-size:0.8rem;color:rgba(255,200,255,0.5);letter-spacing:0.06em;font-weight:600;">{f.label}</span>
        </div>
      {/each}
      <div class="a-reveal" style="margin-top:0.5rem;display:inline-flex;align-items:center;gap:0.6rem;padding:0.6rem 1.2rem;border:1px solid rgba(0,255,100,0.35);border-radius:2rem;background:rgba(0,255,100,0.06);width:fit-content;">
        <span style="width:8px;height:8px;border-radius:50%;background:#00ff64;box-shadow:0 0 8px #00ff64;animation:pulse 2s infinite;"></span>
        <span style="font-size:0.72rem;color:#00ff64;font-weight:700;letter-spacing:0.1em;text-transform:uppercase;text-shadow:0 0 8px #00ff64;">Open to work</span>
      </div>
    </div>
  </div>
</section>

<style>
  @keyframes pulse { 0%,100%{opacity:1} 50%{opacity:0.35} }

  @media (max-width: 768px) {
    .about-section { padding: 4rem 1.5rem !important; }
    .about-grid {
      grid-template-columns: 1fr !important;
      gap: 2.5rem !important;
    }
  }
</style>
