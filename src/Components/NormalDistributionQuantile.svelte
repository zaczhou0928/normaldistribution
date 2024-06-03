<script>
  import { onMount } from 'svelte';
  import * as d3 from 'd3';
  import { jStat } from 'jstat';

  let mean = 0;
  let std = 1;
  let xValue = 0; // Variable for slider control
  let svg;
  let xAxisGroup, yAxisGroup, linePath, areaPath;
  let areaCovered = 0;
  let xScale, yScale;

  function normalDistribution(x, mean, std) {
    return (1 / (std * Math.sqrt(2 * Math.PI))) * Math.exp(-0.5 * ((x - mean) / std) ** 2);
  }

  function cdf(x, mean, std) {
    return jStat.normal.cdf(x, mean, std);
  }

  function setupChart() {
    const margin = { top: 20, right: 20, bottom: 40, left: 50 },
          width = 650 - margin.left - margin.right,
          height = 450 - margin.top - margin.bottom;

    // Set up scales
    xScale = d3.scaleLinear().range([0, width]);
    yScale = d3.scaleLinear().range([height, 0]);

    // Append the svg object to the body of the page
    const g = d3.select(svg)
                .attr("width", width + margin.left + margin.right)
                .attr("height", height + margin.top + margin.bottom)
                .append("g")
                .attr("transform", `translate(${margin.left},${margin.top})`);

    // Create axes groups
    xAxisGroup = g.append("g")
                  .attr("transform", `translate(0,${height})`);
    yAxisGroup = g.append("g");

    // Add the line path
    linePath = g.append("path")
                .attr("fill", "none")
                .attr("stroke", "steelblue")
                .attr("stroke-width", 2);

    // Add the area path
    areaPath = g.append("path")
                .attr("fill", "lightblue");
    // Adding X-axis label
    g.append("text")
      .attr("text-anchor", "end")
      .attr("x", width / 2 + margin.left + 70)
      .attr("y", height + margin.bottom - 5 )
      .text("#Standard Deviations from Mean");

    // Adding Y-axis label
    g.append("text")
      .attr("text-anchor", "end")
      .attr("transform", "rotate(-90)")
      .attr("y", -margin.left + 10)
      .attr("x", -height / 2 + margin.top + 60)
      .text("Probability Density");
  }

  function updateGraph() {
    if (!xScale || !yScale) return; // Ensure scales are defined

    if (std < 0.4) {
      std = 0.4
    }

    if (mean < -6) {
      mean = -6
    }

    if (mean > 6) {
      mean = 6
    }

    const xDomain = [-10, 10];
    xScale.domain(xDomain);
    const data = d3.range(xDomain[0], xDomain[1], (xDomain[1] - xDomain[0]) / 100).map(x => ({
      x,
      y: normalDistribution(x, mean, std)
    }));
    yScale.domain([0, 1]);

    const line = d3.line()
                   .x(d => xScale(d.x))
                   .y(d => yScale(d.y));

    linePath.datum(data).attr("d", line);
    xAxisGroup.call(d3.axisBottom(xScale));
    yAxisGroup.call(d3.axisLeft(yScale).ticks(5));

    // Define the area up to the selected x-value
    const area = d3.area()
                   .x(d => xScale(d.x))
                   .y1(d => yScale(d.y))
                   .y0(yScale(0));

    areaPath.datum(data.filter(d => d.x <= xValue)).attr("d", area);
    areaCovered = cdf(xValue, mean, std);
  }

  onMount(() => {
    setupChart();
    updateGraph(); // Call updateGraph here to ensure initial drawing
  });

  // Reactively update the graph whenever mean, std, or xValue changes
  $: if (mean || std || xValue) updateGraph();
</script>

<p class="body-text">
  What happens if we change the mean or the standard deviation of a normal distribution? Use our interactive model to adjust the mean and standard deviation parameters. As you modify these parameters, observe how the shape of the normal distribution changes.
</p>

<div class="slider-container">
  <label for="mean">Mean:</label>
  <input type="range" id="mean" bind:value={mean} min="-10" max="10" step="0.1">

  <label for="std">Standard Deviation:</label>
  <input type="range" id="std" bind:value={std} min="0.1" max="5" step="0.1">

  <label for="xValue">X-Value:</label>
  <input type="range" id="xValue" bind:value={xValue} min="-10" max="10" step="0.1">

  <p>Mean: {mean}</p>
  <p>Standard Deviation: {std}</p>
  <p>X-Value: {xValue}</p>
  <p>Area Covered: {(areaCovered * 100).toFixed(2)}%</p>
</div>

<!-- SVG container for D3 graph -->
<svg bind:this={svg}></svg>

<div class="content-container">
  <h1 class='body-header'>What Does the Parameters Reflect?</h1>

  <ul class='body-text'>
    <li><strong>Mean (µ):</strong> Shifts the peak of the curve along the x-axis. The mean represents the average value of the dataset, which in this case can be thought of as the average height of high school students.</li>
    <li><strong>Standard Deviation (σ):</strong> Changes the spread of the curve. A larger standard deviation results in a wider curve, indicating more variability in student heights. A smaller standard deviation results in a narrower curve, suggesting that most students' heights are closer to the average.</li>
    <li><strong>X-Value:</strong> Select a specific value along the x-axis. This is useful for seeing how individual data points compare relative to the overall distribution.</li>
    <li><strong>Area Under the Curve:</strong> The shaded area represents the probability of finding a data point below the selected x-value. This area changes dynamically as you adjust the X-Value slider, allowing you to visualize and understand probabilities in a normal distribution context.</li>
  </ul>

  <p class='body-text'>
    Use these interactive tools to deepen your understanding of how statistical measures influence the shape of a normal distribution and what the implications are for real-world data like high school student heights.
  </p>
</div>

<style>
  input {
    margin: 0.5rem;
    padding: 0.2rem;
    width: 80px;
  }
  svg {
    height: 850px;
    overflow: visible;
    display: block;
    margin: 0 auto;
  }

  .slider-container {
    text-align: center; /* Centers the text and inline elements like input */
    margin: 20px auto; /* Adds margin on top and bottom, auto on left and right */
    width: 80%; /* Adjust this as needed to fit the design */
  }

  .content-container {
    margin: 20px auto; /* Centers the container and adds vertical spacing */
    margin-top: -400px; /* Sets the top margin to 20 pixels */
    padding: 20px; /* Adds padding inside the container */
    max-width: 800px; /* Restricts the maximum width to keep the content readable */
    font-size: 18px;
}
</style>
