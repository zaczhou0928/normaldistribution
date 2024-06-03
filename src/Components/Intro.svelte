<script>
  import SimpleNorm from "./SimpleNorm.svelte";
</script>

<article class="content">
  <p class="body-text" style="margin-bottom: 50px">
    The <strong>Normal Distribution</strong>, also known as the Gaussian distribution, is a foundational concept in statistics. This probability distribution is symmetric about the mean, indicating that data near the mean are more frequently observed than data far from the mean. For a more detailed explanation, visit <a href="https://en.wikipedia.org/wiki/Normal_distribution" target="_blank">Wikipedia</a>.
  </p>

  <SimpleNorm />

  <p class="body-text" style="margin-top: -350px">
    Characterized by its bell-shaped curve, the Normal Distribution begins low, peaks at the mean, and then decreases symmetrically. This distinct shape illustrates that occurrences near the mean are more frequent, while those farther from the mean are less common. Its symmetry around the mean implies that deviations to either side are equally probable, emphasizing the central tendency of data to cluster around the mean, with probabilities diminishing symmetrically as values diverge.
  </p>

  <p class="body-text">
    To see the Normal Distribution in action, consider a dataset of high school student heights. As you scroll down, observe how the graph of distributions, with gradually increasing sample sizes, starts to resemble the iconic 'bell curve' of the Normal Distribution as the sample size grows.
  </p>
</article>

<style>
  .content {
  max-width: 800px; /* Ensures optimal line length for readability */
  margin: 0 auto; /* Centers the content */
}

strong {
  font-weight: bold; /* Ensures 'strong' tags are bold */
}

a {
  color: #0077cc; /* Sets a standard color for links */
  text-decoration: none; /* Removes underline from links */
}

.body-text {
    margin-bottom: 10px;  /* Adds space between paragraphs */
  }

</style>