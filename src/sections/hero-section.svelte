<script>
  import { onMount } from "svelte";
  import gsap from "gsap";

  let tagline, heading, sub, photo, scrollCue;
  const words = ["Zoltan", "Debreceni"];
  const stack = ["React Native","Flutter","GCP · Firebase","AWS · K8s","TypeScript","Node.js"];

  onMount(() => {
    const tl = gsap.timeline({ delay: 0.4 });
    tl.fromTo(tagline, { y:16,opacity:0 }, { y:0,opacity:1,duration:0.7,ease:"power2.out" })
      .fromTo(heading.querySelectorAll(".word"), { y:"110%",opacity:0 }, { y:"0%",opacity:1,duration:0.9,stagger:0.1,ease:"power4.out" }, "-=0.4")
      .fromTo(sub.children, { y:18,opacity:0 }, { y:0,opacity:1,duration:0.6,stagger:0.07,ease:"power2.out" }, "-=0.3")
      .fromTo(photo, { scale:1.06,opacity:0 }, { scale:1,opacity:1,duration:1,ease:"power3.out" }, "-=0.5")
      .fromTo(scrollCue, { opacity:0 }, { opacity:1,duration:0.5 }, "-=0.2");

    gsap.to(scrollCue, { y:7,repeat:-1,yoyo:true,duration:1,ease:"sine.inOut" });
  });
</script>

<section id="header" class="hero-section" style="
  min-height:100svh; display:flex; align-items:center;
  position:relative; overflow:hidden; padding:6rem 2.5rem 4rem;
  background: linear-gradient(160deg, #0d001a 0%, #1a0040 35%, #2d0060 60%, #1a003a 80%, #0d001a 100%);
">
  <!-- diagonal grid SVG (from original) -->
  <div style="position:absolute;inset:0;z-index:0;pointer-events:none;opacity:0.4;
    background-image:url('data:image/svg+xml;charset=utf8,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%20512%20512%22%20width%3D%22512%22%20height%3D%22512%22%20preserveAspectRatio%3D%22none%22%3E%20%3Cstyle%3E%20line%20%7B%20stroke-linecap%3A%20square%3B%20stroke-width%3A%202.01px%3B%20stroke%3A%20rgba(255,87,238,0.15)%3B%20vector-effect%3A%20non-scaling-stroke%3B%20%7D%20%3C%2Fstyle%3E%20%3Cline%20x1%3D%22256%22%20y1%3D%220%22%20x2%3D%220%22%20y2%3D%22256%22%20%2F%3E%20%3Cline%20x1%3D%22256%22%20y1%3D%22512%22%20x2%3D%22512%22%20y2%3D%22256%22%20%2F%3E%3C%2Fsvg%3E');
    background-size:80px 80px;">
  </div>

  <!-- retro sun -->
  <div style="position:absolute;bottom:30%;left:50%;transform:translateX(-50%);
    width:clamp(200px,32vw,380px);aspect-ratio:1;border-radius:50%;z-index:1;pointer-events:none;
    background:linear-gradient(to bottom,#ff9f00 0%,#ff4fa3 45%,#9400ff 100%);
    box-shadow:0 0 100px 30px #ff4fa366,0 0 200px 80px #9400ff22;overflow:hidden;">
    {#each Array(9) as _,i}
      <div style="position:absolute;left:0;right:0;height:5%;background:linear-gradient(160deg,#0d001a,#1a0040);top:{52+i*6}%;"></div>
    {/each}
  </div>

  <!-- horizon grid -->
  <div style="position:absolute;bottom:0;left:0;right:0;height:38%;z-index:2;pointer-events:none;
    background-image:linear-gradient(#ff00ff33 1px,transparent 1px),linear-gradient(90deg,#ff00ff22 1px,transparent 1px);
    background-size:55px 38px;
    -webkit-mask-image:linear-gradient(to top,rgba(0,0,0,0.85) 0%,transparent 100%);
    mask-image:linear-gradient(to top,rgba(0,0,0,0.85) 0%,transparent 100%);
    transform:perspective(380px) rotateX(52deg);transform-origin:bottom center;">
  </div>

  <!-- scanlines -->
  <div style="position:absolute;inset:0;z-index:3;pointer-events:none;
    background:repeating-linear-gradient(0deg,rgba(0,0,0,0.07) 0px,rgba(0,0,0,0.07) 1px,transparent 1px,transparent 3px);">
  </div>

  <!-- left content -->
  <div class="hero-text" style="flex:1;position:relative;z-index:10;max-width:580px;">
    <p bind:this={tagline} style="font-size:0.7rem;letter-spacing:0.28em;text-transform:uppercase;color:#ff9f00;margin-bottom:1.5rem;font-weight:700;text-shadow:0 0 16px #ff9f0099;">
      Fullstack Engineer
    </p>
    <h1 bind:this={heading} style="font-size:clamp(3rem,7.5vw,7.5rem);font-weight:900;letter-spacing:-0.03em;line-height:0.95;color:#fff;margin-bottom:2.5rem;text-shadow:0 0 60px #ff4fa344,0 0 120px #9400ff22;">
      {#each words as word}
        <span style="display:block;overflow:hidden;">
          <span class="word" style="display:block;">{word}</span>
        </span>
      {/each}
    </h1>
    <div bind:this={sub} style="display:flex;flex-direction:column;gap:1.2rem;">
      <p style="font-size:0.95rem;color:rgba(255,220,255,0.55);line-height:1.65;max-width:400px;">
        Building mobile & web experiences with React Native, Flutter, and cloud infra on GCP & Firebase.
      </p>
      <div style="display:flex;flex-wrap:wrap;gap:0.45rem;margin-top:0.4rem;">
        {#each stack as item}
          <span style="font-size:0.68rem;padding:0.28rem 0.85rem;border-radius:2rem;border:1px solid rgba(255,159,0,0.4);color:#ff9f00;letter-spacing:0.07em;font-weight:600;background:rgba(255,159,0,0.08);text-shadow:0 0 8px #ff9f0066;">
            {item}
          </span>
        {/each}
      </div>
    </div>
  </div>

  <!-- photo -->
  <div bind:this={photo} class="hero-photo" style="flex-shrink:0;width:clamp(200px,26vw,340px);aspect-ratio:3/4;border-radius:0.75rem;
    background:linear-gradient(145deg,#1a0040,#2d0060);
    border:1px solid rgba(255,79,163,0.4);
    display:flex;align-items:center;justify-content:center;
    position:relative;overflow:hidden;margin-left:3rem;z-index:10;
    box-shadow:0 0 40px rgba(255,79,163,0.25),0 0 80px rgba(148,0,255,0.15),0 30px 80px rgba(0,0,0,0.6);">
    <div style="position:absolute;top:0.6rem;left:0.6rem;width:1.2rem;height:1.2rem;border-top:2px solid #ff4fa3;border-left:2px solid #ff4fa3;border-radius:2px;"></div>
    <div style="position:absolute;top:0.6rem;right:0.6rem;width:1.2rem;height:1.2rem;border-top:2px solid #ff9f00;border-right:2px solid #ff9f00;border-radius:2px;"></div>
    <div style="position:absolute;bottom:0.6rem;left:0.6rem;width:1.2rem;height:1.2rem;border-bottom:2px solid #ff9f00;border-left:2px solid #ff9f00;border-radius:2px;"></div>
    <div style="position:absolute;bottom:0.6rem;right:0.6rem;width:1.2rem;height:1.2rem;border-bottom:2px solid #ff4fa3;border-right:2px solid #ff4fa3;border-radius:2px;"></div>
    <div style="text-align:center;color:rgba(255,150,220,0.2);position:relative;z-index:1;">
      <div style="font-size:3.5rem;margin-bottom:0.5rem;">👤</div>
      <p style="font-size:0.65rem;letter-spacing:0.15em;text-transform:uppercase;">Photo coming</p>
    </div>
    <div style="position:absolute;bottom:0;left:0;right:0;height:3px;background:linear-gradient(90deg,#9400ff,#ff4fa3,#ff9f00);box-shadow:0 0 12px #ff4fa3;"></div>
    <div style="position:absolute;inset:0;pointer-events:none;background:repeating-linear-gradient(0deg,rgba(0,0,0,0.1) 0px,rgba(0,0,0,0.1) 1px,transparent 1px,transparent 3px);"></div>
  </div>

  <!-- scroll cue -->
  <div bind:this={scrollCue} style="position:absolute;bottom:2rem;left:50%;transform:translateX(-50%);display:flex;flex-direction:column;align-items:center;gap:0.5rem;color:#ff9f0066;font-size:0.65rem;letter-spacing:0.2em;text-transform:uppercase;z-index:10;text-shadow:0 0 10px #ff9f00;">
    <div style="width:1px;height:2rem;background:linear-gradient(to bottom,transparent,#ff9f0066);"></div>
    scroll
  </div>
</section>

<style>
  @media (max-width: 768px) {
    .hero-section {
      flex-direction: column-reverse !important;
      justify-content: flex-end !important;
      padding: 5rem 1.5rem 3rem !important;
      gap: 2rem;
    }
    .hero-photo {
      width: 140px !important;
      aspect-ratio: 1 !important;
      border-radius: 50% !important;
      margin-left: 0 !important;
      align-self: center;
    }
    .hero-text {
      max-width: 100% !important;
    }
  }
</style>
