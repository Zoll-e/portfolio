<script lang="ts">
  import { onMount } from "svelte";
  import gsap from "gsap";
  import { ScrollTrigger } from "gsap/ScrollTrigger";
  gsap.registerPlugin(ScrollTrigger);

  const projects = [
    { num:"01", title:"Coming soon",  type:"???",                   year:"2025", color:"#ff00ff", image:"", url:"" },
    { num:"02", title:"SkillMate",    type:"Web · React / Node.js", year:"2024", color:"#ff9f43", image:"/images/skillmate.png",  url:"https://skillmateapp.com/"  },
    { num:"03", title:"Acasus",       type:"Web · React / Next.js", year:"2023", color:"#bf5fff", image:"/images/acasus.png",     url:"https://acasus.com/"        },
    { num:"04", title:"MyEnergi",     type:"Web · React / Next.js", year:"2023", color:"#00ff88", image:"/images/myenergi.png",   url:"https://www.myenergi.com/"  },
    { num:"05", title:"HelloMoso",    type:"Web · React / Next.js", year:"2024", color:"#00ffff", image:"/images/hellomoso.png",  url:"https://hellomoso.hu/"      },
  ];

  const rotations = [-4, 2, -2, 5, -6];
  let section: HTMLElement;

  // module-level ref persists across HMR — guarantees cleanup before recreate
  let _tl: gsap.core.Timeline | null = null;
  function killPrev() {
    if (_tl) { _tl.scrollTrigger?.kill(); _tl.kill(); _tl = null; }
    ScrollTrigger.getById("projects-pin")?.kill();
    // remove any orphaned pin-spacer divs from previous HMR cycle
    document.querySelectorAll('.pin-spacer').forEach(spacer => {
      if (spacer.querySelector('#projects')) spacer.replaceWith(...Array.from(spacer.children));
    });
  }

  function zoomOpen(url: string, cardEl: HTMLElement) {
    const imgEl = cardEl.querySelector<HTMLImageElement>('[data-img]');
    if (!imgEl) return;
    const rect = imgEl.getBoundingClientRect();
    const clone = document.createElement('img');
    clone.src = imgEl.src;
    clone.style.cssText = `position:fixed;z-index:99999;margin:0;padding:0;border:none;top:${rect.top}px;left:${rect.left}px;width:${rect.width}px;height:${rect.height}px;object-fit:cover;border-radius:0.75rem;pointer-events:none;`;
    document.body.appendChild(clone);
    gsap.to(clone, {
      top:0,left:0,width:window.innerWidth,height:window.innerHeight,borderRadius:0,
      duration:0.75,ease:'power3.inOut',
      onComplete:()=>{
        window.open(url,'_blank');
        gsap.to(clone,{opacity:0,duration:0.5,delay:0.15,onComplete:()=>clone.remove()});
      },
    });
  }

  onMount(() => {
    const cards = Array.from(section.querySelectorAll<HTMLElement>('.stack-card'));
    const total = cards.length;

    cards.forEach((card, i) => {
      gsap.set(card, { xPercent:-50, yPercent:-50, rotation:rotations[i], scale:1-(total-1-i)*0.04, zIndex:i+1 });
    });

    killPrev();

    const tl = gsap.timeline({
      scrollTrigger: {
        id: "projects-pin",
        trigger: section,
        start: "top top",
        end: ()=>`+=${total*700 + 600}`,
        scrub: 1.2,
        pin: true,
        pinSpacing: true,
        anticipatePin: 1,
      },
    });

    for (let i = total-1; i > 0; i--) {
      tl.to(cards[i], { xPercent:-180, yPercent:-70, rotation:rotations[i]-35, opacity:0, duration:1, ease:"power2.in" });
      tl.to(cards[i-1], { scale:1, rotation:rotations[i-1]*0.25, duration:1, ease:"power2.out" }, "<0.15");
      tl.to({}, { duration:0.35 });
    }

    // linger on the last card before releasing scroll
    tl.to({}, { duration: .8 });

    _tl = tl;
    return () => killPrev();
  });
</script>

<section bind:this={section} id="projects" style="
  height:100svh; overflow:hidden; position:relative;
  background:linear-gradient(135deg,#160830 0%,#220a40 40%,#1a0635 70%,#100520 100%);
">

  <div style="position:absolute;inset:0;z-index:0;pointer-events:none;
    background-image:url('data:image/svg+xml;charset=utf8,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20viewBox%3D%220%200%20512%20512%22%20width%3D%22512%22%20height%3D%22512%22%20preserveAspectRatio%3D%22none%22%3E%20%3Cstyle%3E%20line%20%7B%20stroke-linecap%3A%20square%3B%20stroke-width%3A%202.01px%3B%20stroke%3A%20rgba(255,0,255,0.1)%3B%20vector-effect%3A%20non-scaling-stroke%3B%20%7D%20%3C%2Fstyle%3E%20%3Cline%20x1%3D%22256%22%20y1%3D%220%22%20x2%3D%220%22%20y2%3D%22256%22%20%2F%3E%20%3Cline%20x1%3D%22256%22%20y1%3D%22512%22%20x2%3D%22512%22%20y2%3D%22256%22%20%2F%3E%3C%2Fsvg%3E');
    background-size:80px 80px;"></div>
  <div style="position:absolute;inset:0;z-index:1;pointer-events:none;background:repeating-linear-gradient(0deg,rgba(0,0,0,0.07) 0px,rgba(0,0,0,0.07) 1px,transparent 1px,transparent 3px);"></div>

  <div style="position:absolute;top:2rem;left:2.5rem;z-index:50;">
    <p style="font-size:0.65rem;letter-spacing:0.22em;text-transform:uppercase;color:#ff00ff88;margin-bottom:0.35rem;font-weight:700;text-shadow:0 0 10px #ff00ff;">Selected work</p>
    <h2 style="font-size:clamp(1.6rem,3.5vw,2.8rem);font-weight:900;color:#fff;letter-spacing:-0.03em;text-shadow:0 0 30px #ff00ff33;">Projects</h2>
  </div>
  <p style="position:absolute;top:2.5rem;right:2.5rem;z-index:50;font-size:0.7rem;color:#ff00ff55;letter-spacing:0.12em;font-weight:600;">{projects.length} projects — scroll</p>

  <div style="position:absolute;inset:0;z-index:10;">
    {#each projects as p}
      <div class="stack-card"
        onclick={(e)=>p.url&&zoomOpen(p.url,e.currentTarget as HTMLElement)}
        style="position:absolute;top:50%;left:50%;width:min(480px,85vw);height:min(340px,58vh);border-radius:0.75rem;border:1px solid {p.color}55;background:linear-gradient(135deg,#0d0020,#1a0035);box-shadow:0 0 30px {p.color}22,0 0 60px {p.color}11,0 30px 70px rgba(0,0,0,0.7);overflow:hidden;display:flex;flex-direction:column;will-change:transform,opacity;cursor:{p.url?'pointer':'default'};"
      >
        <div style="flex:1;background:linear-gradient(135deg,#130025,#1f003a,{p.color}18);position:relative;display:flex;align-items:center;justify-content:center;overflow:hidden;">
          {#if p.image}
            <img data-img src={p.image} alt={p.title} style="position:absolute;inset:0;width:100%;height:100%;object-fit:cover;z-index:1;" />
            <div style="position:absolute;top:0.7rem;right:0.7rem;z-index:20;font-size:0.58rem;color:{p.color};background:{p.color}18;border:1px solid {p.color}55;padding:0.18rem 0.55rem;border-radius:1rem;letter-spacing:0.1em;font-weight:700;">↗ VISIT</div>
          {:else}
            <div style="width:60px;height:60px;border-radius:50%;border:1px dashed {p.color}50;display:flex;align-items:center;justify-content:center;color:{p.color}50;font-size:1.4rem;z-index:2;">+</div>
          {/if}
          <div style="position:absolute;top:0.8rem;left:0.8rem;width:1rem;height:1rem;border-top:2px solid {p.color};border-left:2px solid {p.color};z-index:5;"></div>
          <div style="position:absolute;top:0.8rem;right:0.8rem;width:1rem;height:1rem;border-top:2px solid {p.color};border-right:2px solid {p.color};z-index:5;"></div>
          <div style="position:absolute;bottom:0.8rem;left:0.8rem;width:1rem;height:1rem;border-bottom:2px solid {p.color};border-left:2px solid {p.color};z-index:5;"></div>
          <div style="position:absolute;bottom:0.8rem;right:0.8rem;width:1rem;height:1rem;border-bottom:2px solid {p.color};border-right:2px solid {p.color};z-index:5;"></div>
          <span style="position:absolute;top:0.8rem;left:1rem;font-size:5rem;font-weight:900;line-height:1;color:{p.color}{p.image?'08':'10'};letter-spacing:-0.04em;pointer-events:none;user-select:none;z-index:3;">{p.num}</span>
          <div style="position:absolute;bottom:0;left:0;right:0;height:2px;background:linear-gradient(90deg,transparent,{p.color},transparent);box-shadow:0 0 10px {p.color};z-index:6;"></div>
          <div style="position:absolute;inset:0;pointer-events:none;background:repeating-linear-gradient(0deg,rgba(0,0,0,0.06) 0px,rgba(0,0,0,0.06) 1px,transparent 1px,transparent 3px);z-index:4;"></div>
        </div>
        <div style="padding:0.9rem 1.3rem 1rem;background:#0a0018;border-top:1px solid {p.color}30;display:flex;justify-content:space-between;align-items:flex-end;">
          <div>
            <p style="font-size:1rem;font-weight:800;color:#fff;letter-spacing:-0.01em;margin-bottom:0.15rem;text-shadow:0 0 20px {p.color}44;">{p.title}</p>
            <p style="font-size:0.68rem;color:{p.color}80;letter-spacing:0.08em;">{p.type}</p>
          </div>
          <span style="font-size:0.62rem;color:{p.color};font-weight:700;letter-spacing:0.12em;border:1px solid {p.color}50;padding:0.18rem 0.6rem;border-radius:1rem;background:{p.color}0d;text-shadow:0 0 8px {p.color};">{p.year}</span>
        </div>
      </div>
    {/each}
  </div>

  <div style="position:absolute;bottom:2.5rem;left:50%;transform:translateX(-50%);display:flex;gap:0.5rem;z-index:50;">
    {#each projects as _,i}
      <div style="width:0.35rem;height:0.35rem;border-radius:50%;background:rgba(255,0,255,{i===projects.length-1?'1':'0.2'});box-shadow:{i===projects.length-1?'0 0 6px #ff00ff':'none'};"></div>
    {/each}
  </div>
</section>
