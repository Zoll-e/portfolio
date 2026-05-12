<script lang="ts">
  import { onMount } from "svelte";
  import gsap from "gsap";
  import { cardData, type CardData } from "../data/card-data";
  import NextButton from "./next-button.svelte";
  import BackButton from "./back-button.svelte";

  export let card: CardData;
  const { id, title, description, image } = card;
  const nextId = id >= cardData.length ? "contact" : `reflection-${id + 1}`;
  const prevId = id === 1 ? "feedbacks" : `reflection-${id - 1}`;
  const isRightPicture = id % 2 === 0;

  let cardEl: HTMLElement;
  let imgEl: HTMLImageElement;
  let textEl: HTMLElement;
  let animated = false;

  onMount(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting && !animated) {
            animated = true;

            gsap.fromTo(cardEl,
              { y: 50, opacity: 0 },
              { y: 0, opacity: 1, duration: 0.8, ease: "power3.out" }
            );
            gsap.fromTo(imgEl,
              { scale: 1.08 },
              { scale: 1, duration: 1.2, ease: "power2.out" }
            );
            gsap.fromTo(Array.from(textEl.children),
              { y: 20, opacity: 0 },
              { y: 0, opacity: 1, duration: 0.6, stagger: 0.1, ease: "power2.out", delay: 0.15 }
            );

            observer.disconnect();
          }
        });
      },
      { threshold: 0.15 }
    );

    observer.observe(cardEl);
    return () => observer.disconnect();
  });
</script>

<div
  bind:this={cardEl}
  id={`reflection-${id}`}
  class={`lg:h-[70vh] h-fit lg:w-7/12 mx-auto mt-10 lg:mt-32 mb-10 lg:mb-32 rounded-xl flex lg:flex-row space-y-3 lg:pb-0 pb-10 lg:space-y-0 flex-col bg-gray-800 shadow-2xl transition-all duration-300 hover:shadow-3xl hover:scale-[1.01] ${
    isRightPicture && "lg:flex-row-reverse"
  }`}
>
  <div class="flex-1 lg:w-1/2 overflow-hidden"
    class:rounded-l-xl={!isRightPicture}
    class:rounded-r-xl={isRightPicture}
    class:rounded-t-xl={true}
  >
    <img
      bind:this={imgEl}
      src={image}
      alt={title}
      class={`${isRightPicture ? "lg:rounded-r-xl lg:rounded-tl-none" : "lg:rounded-l-xl lg:rounded-tr-none"} rounded-t-xl flex-1 lg:h-[70vh] w-full bg-gray-500 object-cover transition-transform duration-500 hover:scale-110`}
    />
  </div>

  <div class={`flex-1 self-center lg:w-1/2 rounded-b-xl mx-auto space-y-10 ${isRightPicture ? "lg:rounded-r-xl" : "lg:rounded-l-xl"}`}>
    <div bind:this={textEl} class="text-white px-10 space-y-5 lg:space-y-10">
      <h3 class="text-white text-2xl tracking-widest font-bold lg:text-3xl">{title}</h3>
      <p style="color: rgba(255,255,255,0.75); line-height: 1.75;">
        {@html description.replace(/\n/g, "<br /><br />")}
      </p>
      <div class="flex justify-between w-full gap-4">
        <BackButton id={prevId} />
        <NextButton id={nextId} />
      </div>
    </div>
  </div>
</div>
