<script>
  import Scrolly from "./Scrolly.svelte";
  import NormalDist from "./NormalDistribution.svelte";
  import NormalDistQ from "./NormalDistributionQuantile.svelte";
  import katexify from "../katexify";
  import { select, selectAll } from "d3-selection";

  // scroll iterator
  let value;

  // Paragraph text for scrolly
  $: steps = [
    `<h1 class='step-title'>Adjust Mean and Standard Deviation</h1>
<p>
  What happens if we change the mean or the standard deviation of a normal distribution? Use our interactive model to adjust the mean and standard deviation parameters. As you modify these parameters, observe how the shape of the normal distribution changes. This hands-on experience helps to understand the impact of these parameters on the population distribution.
</p>`,
    `<h1 class='step-title'>What Does the Area Represent?</h1>
<p>
  Here we have a more detailed graph of a standard normal distribution to help you understand what this probability density function can inform us. Adjust the sliders above to manipulate key parameters and observe their impact:
</p>

<ul>
  <li><strong>Mean (µ):</strong> Shifts the peak of the curve along the x-axis. The mean represents the average value of the dataset, which in this case can be thought of as the average height of high school students.</li>
  <li><strong>Standard Deviation (σ):</strong> Changes the spread of the curve. A larger standard deviation results in a wider curve, indicating more variability in student heights. A smaller standard deviation results in a narrower curve, suggesting that most students' heights are closer to the average.</li>
  <li><strong>X-Value:</strong> Select a specific value along the x-axis. This is useful for seeing how individual data points compare relative to the overall distribution.</li>
  <li><strong>Area Under the Curve:</strong> The shaded area represents the probability of finding a data point below the selected x-value. This area changes dynamically as you adjust the X-Value slider, allowing you to visualize and understand probabilities in a normal distribution context.</li>
</ul>

<p>
  Use these interactive tools to deepen your understanding of how statistical measures influence the shape of a normal distribution and what the implications are for real-world data like high school student heights.
</p>
  `,
  ];

  const target2event = {
    0: () => {},
    1: () => {},
    2: () => {},
  };

  $: if (typeof value !== "undefined") target2event[value]();
</script>

<h2 class="body-header">Interactive Visualization of Normal Distribution</h2>
<p class="body-text">
  Below are two interactive graphs of normal distribution. You can freely choose parameters to visualize how they interact with each others and their impact on normal distribution.
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
        <NormalDist />
      {:else if value === 1}
        <NormalDistQ />
      {/if}
    </div>
  </div>
  <br /><br />
  <p class="body-text"></p>
</section>

<style>
  /* space after scroll is finished */
  .spacer {
    height: 40vh;
  }

  .charts-container {
    position: sticky;
    top: 10%;
    background: var(--bg);
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
    color: var(--bg);
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
  }

  .step.active .step-content {
    background: #f7e8e4;
    color: var(--squid-ink);
    border: 2px solid var(--default);
  }

  .steps-container {
    height: 100%;
  }

  .steps-container {
    flex: 1 1 40%;
    z-index: 10;
  }

  /* Comment out the following line to always make it 'text-on-top' */
  @media screen and (max-width: 950px) {
    .section-container {
      flex-direction: column-reverse;
    }

    .steps-container {
      pointer-events: none;
    }

    .charts-container {
      top: 7.5%;
      width: 95%;
      margin: auto;
    }

    .step {
      height: 130vh;
    }

    .step-content {
      width: 95%;
      max-width: 768px;
      font-size: 18px;
      line-height: 2;
    }

    .spacer {
      height: 100vh;
    }
  }
</style>
