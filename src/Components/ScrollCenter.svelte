<script>
  import Scrolly from "./Scrolly.svelte";
  import Sample10 from "./Sample10.svelte";
  import Sample50 from "./Sample50.svelte";
  import Sample100 from "./Sample100.svelte";
  import Sample1000 from "./Sample1000.svelte";
  import SampleAll from "./SampleAll.svelte";
  import Histogram from "./Histogram.svelte";

  // scroll iterator
  let value;

  // Paragraph text for scrolly
  $: steps = [
    `<h1 class='step-title'>Sample Size = 10</h1>
    <p>When we only have 10 values of heights in our sample, the distribution is more like a uniform distribution rather than a normal distribuition.</p>`,
    `<h1 class='step-title'>Sample Size = 50</h1>
    <p>Increasing sample size from 10 to 50 makes our sample distribution getting closer to the shape of a normal distribution.</p>`,
    `<h1 class='step-title'>Sample Size = 100</h1>
    <p></p>`,
    `<h1 class='step-title'>Sample Size = 1000</h1>
    <p>With a sample size of 1000, we can clearly see that our sample distribution resembles a normal distribution quite well.</p>`,
    `<h1 class='step-title'>Sample Size = Population</h1>
    <p>With full population, we would reach optimal shape of a normal distribution, given our population size is statistically significant.</p>`
  ];

  const target2event = {
    0: () => { /* Define interactions for step 0 */ },
    1: () => { /* Define interactions for step 1 */ },
    2: () => { /* Define interactions for step 2 */ },
    3: () => { /* Define interactions for step 3 */ },
    4: () => { /* Define interactions for step 4 */ },
    5: () => { /* Define interactions for step 5 */ },
    6: () => { /* Define interactions for step 6 */ }
  };

  // trigger events on scroll typeof lastname !== "undefined"
  // $: if (value) target2event[value]()
  $: if (typeof value !== "undefined") target2event[value]();
</script>

<p class="body-text">
</p>

<section>
  <!-- scroll container -->
  <div class="section-container">
    <div class="steps-container">
      <Scrolly bind:value>
        {#each steps as text, i}
          <div class="step" class:active={value === i}>
            <div class="step-content">{@html text}</div>
          </div>
        {/each}
        <div class="spacer" />
      </Scrolly>
    </div>
    <div class="charts-container">
      {#if value === 0}
        <Sample10 />
      {:else if value === 1}
        <Sample50 />
      {:else if value === 2}
        <Sample100 />
      {:else if value === 3}
        <Sample1000 />
      {:else if value === 4}
        <SampleAll />
      {:else if value >= 5}
        <Histogram />
      {/if}
    </div>
  </div>
</section>

<style>
  /* space after scroll is finished */
  .spacer {
    height: 40vh;
  }

  .charts-container {
    position: sticky;
    top: 10%;
    display: grid;
    width: 50%;
    grid-template-columns: 100%;
    grid-row-gap: 2rem;
    grid-column-gap: 0rem;
    grid-template-rows: repeat(2, 1fr);
    height: 85vh;
  }

  .section-container {
    margin-top: 1em;
    text-align: center;
    transition: background 100ms;
    display: flex;
  }

  .step {
    height: 110vh;
    display: flex;
    place-items: center;
    justify-content: center;
  }

  .step-content {
    font-size: 18px;
    background: var(--bg);
    color: #ccc;
    border-radius: 1px;
    padding: 0.5rem 1rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    transition: background 500ms ease;
    text-align: left;
    width: 75%;
    margin: auto;
    max-width: 500px;
    font-family: var(--font-main);
    line-height: 1.3;
    border: 2px solid var(--default);
  }

  .step.active .step-content {
    background: #f1f3f3ee;
    color: var(--squid-ink);
  }

  .steps-container {
    height: 100%;
  }

  .steps-container {
    flex: 1 1 40%;
    z-index: 10;
  }

  /* make side centered */
  .section-container {
    flex-direction: column-reverse;
  }

  .steps-container {
    pointer-events: none;
  }

  .charts-container {
    top: 7.5%;
    width: 75%;
    margin: auto;
  }

  .step {
    height: 130vh;
  }

  .step-content {
    width: 65%;
    max-width: 768px;
    font-size: 17px;
    line-height: 1.6;
  }

  .spacer {
    height: 100vh;
  }
</style>
