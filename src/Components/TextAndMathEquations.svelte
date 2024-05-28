<script>
  let answer1 = '';
  let answer2 = '';
  let answer3 = '';
  let answer4 = '';
  let answer5 = ''; // Added for the new question
  let showAnswers = false; // This variable will control the display of the correct answers

  function toggleAnswers() {
    showAnswers = !showAnswers; // Toggle the display of the answers
  }
</script>

<style>
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    margin-top: 50px;
  }

  .question {
    margin-bottom: 40px;
  }

  .options, .answer {
    display: block;
    margin: 10px 0;
    font-size: 16px;
  }

  label {
    margin-bottom: 5px;
    display: block;
  }

  input[type="radio"] {
    margin-right: 10px;
  }
</style>

<div class="container">
  <h1>Quiz Time!</h1>
  <div class="question">
    <p>True or False: In a normal distribution, the mean, median, and mode all have the same value and the graph of the distribution is symmetric.</p>
    <label>
      <input type="radio" bind:group={answer1} value="true"> True
    </label>
    <label>
      <input type="radio" bind:group={answer1} value="false"> False
    </label>
  </div>
  
  <div class="question">
    <p>What 2 population parameters determine the shape of the normal curve? (they make the curve tall and skinny or short and fat)</p>
    <label class="option">
      <input type="radio" bind:group={answer2} value="a"> a, median and mean
    </label>
    <label class="option">
      <input type="radio" bind:group={answer2} value="b"> b, mode and standard deviation
    </label>
    <label class="option">
      <input type="radio" bind:group={answer2} value="c"> c, median and standard deviation
    </label>
    <label class="option">
      <input type="radio" bind:group={answer2} value="d"> d, mean and mode
    </label>
    <label class="option">
      <input type="radio" bind:group={answer2} value="e"> e, mean and standard deviation
    </label>
  </div>
  
  <div class="question">
    <p>Which of the following distributions is the least likely to fit a normal distribution?</p>
    <label class="option">
      <input type="radio" bind:group={answer3} value="a"> a, distribution of the heights of professional soccer players
    </label>
    <label class="option">
      <input type="radio" bind:group={answer3} value="b"> b, distribution of the lengths of salmon in the Pacific Ocean
    </label>
    <label class="option">
      <input type="radio" bind:group={answer3} value="c"> c, distribution of test scores among those who took the SATs in 1998
    </label>
    <label class="option">
      <input type="radio" bind:group={answer3} value="d"> d,distribution of the ages of automobiles in driveable condition
    </label>
    <label class="option">
      <input type="radio" bind:group={answer3} value="e"> e, distribution of the points scored by a basketball player per game
    </label>
  </div>
  
  <div class="question">
    <p>True or False: The point where the tails of a normal curve reach the x-axis is the exact point where the upper and lower extremes of the population are located.</p>
    <label>
      <input type="radio" bind:group={answer4} value="true"> True
    </label>
    <label>
      <input type="radio" bind:group={answer4} value="false"> False
    </label>
  </div>

  <!-- Button to show answers -->
  <button on:click={toggleAnswers}>Show Answers</button>

  <!-- Conditional display of answers -->
  {#if showAnswers}
    <div class="answers">
      <p>Answers:</p>
      <p>1: True (T)</p>
      <p>2: a, median and mean (A)</p>
      <p>3: d, distribution of the ages of automobiles in drivable condition (D)</p>
      <p>4: False (F)</p>
    </div>
  {/if}
</div>

