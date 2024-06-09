<script>
  import { onMount } from 'svelte';
  import * as d3 from 'd3';
  import { heightData } from "../heightdata.js";

  const selectedSampleSize = 100;
  const sampledData = heightData.slice(0, selectedSampleSize);

  function normalDistribution(x, mean, sigma) {
    const sqrt2pi = Math.sqrt(2 * Math.PI);
    return (1 / (sigma * sqrt2pi)) * Math.exp(-0.5 * Math.pow((x - mean) / sigma, 2));
  }

  function setupChart() {
    const margin = { top: 20, right: 40, bottom: 40, left: 50 };
    const width = 600 - margin.left - margin.right;
    const height = 400 - margin.top - margin.bottom;

    const container = d3.select('#custom-chart-container100')
      .select("svg")
      .remove(); // Remove any existing chart

    const svg = d3.select('#custom-chart-container100')
      .append('svg')
      .attr('width', width + margin.left + margin.right)
      .attr('height', height + margin.top + margin.bottom)
      .append('g')
      .attr('transform', `translate(${margin.left},${margin.top})`);

    const heights = sampledData.map(d => d["Height(Inches)"]);
    const mean = d3.mean(heights);
    const stdDev = d3.deviation(heights);

    const bins = d3.histogram()
      .domain(d3.extent(heights))
      .thresholds(d3.range(60, 85, 0.5))
      (heights);

    const xScale = d3.scaleLinear()
      .domain([55, 82]) // Extended to better fit the distribution
      .range([0, width]);

    const yScale = d3.scaleLinear()
      .domain([0, d3.max(bins, d => d.length)])
      .range([height, 0]);

    svg.selectAll('rect')
      .data(bins)
      .enter().append('rect')
      .attr('x', d => xScale(d.x0))
      .attr('y', d => yScale(d.length))
      .attr('width', d => xScale(d.x1) - xScale(d.x0) - 1)
      .attr('height', d => height - yScale(d.length))
      .attr('fill', 'steelblue');

    // Normalize the PDF to fit within the histogram scale
    const pdfScaleFactor = d3.max(bins, d => d.length) / normalDistribution(mean, mean, stdDev);

    const line = d3.line()
      .x(d => xScale(d))
      .y(d => yScale(normalDistribution(d, mean, stdDev) * pdfScaleFactor))
      .curve(d3.curveBasis);

    const points = d3.range(55, 82, 0.1);
    svg.append("path")
      .datum(points)
      .attr("fill", "none")
      .attr("stroke", "red")
      .attr("d", line);

    svg.append('g')
      .attr('transform', `translate(0,${height})`)
      .call(d3.axisBottom(xScale));

    svg.append('g')
      .call(d3.axisLeft(yScale));

    svg.append('text')
      .attr('x', width / 2)
      .attr('y', height + margin.bottom - 5)
      .attr('text-anchor', 'middle')
      .text('Height (inches)');

    svg.append('text')
      .attr('transform', 'rotate(-90)')
      .attr('x', -height / 2)
      .attr('y', -margin.left + 20)
      .attr('text-anchor', 'middle')
      .text('Frequency');
  }

  onMount(() => {
    setupChart();
  });
</script>

<div id="custom-chart-container100"></div>

<style>
  #custom-chart-container100 {
    width: 600px;
    height: 400px;
    margin-left: auto;
    margin-right: auto;
  }
</style>

