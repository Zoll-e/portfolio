<script>
  import Navbar        from "../components/navbar.svelte";
  import Footer        from "../components/footer.svelte";
  import Hero          from "../sections/hero-section.svelte";
  import About         from "../sections/about.svelte";
  import StackingCards from "../sections/stacking-cards.svelte";
  import TechStack     from "../sections/tech-stack.svelte";
  import Contact       from "../sections/contact.svelte";
</script>

<Navbar />
<Hero />
<About />
<StackingCards />
<TechStack />
<Contact />
<Footer />

<style>
  :global(html), :global(body) {
    width: 100%;
    overflow-x: hidden;
    font-family: "Inter", system-ui, sans-serif;
    background: #0d001a;
  }
</style>
