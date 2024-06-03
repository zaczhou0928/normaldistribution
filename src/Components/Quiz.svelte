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
    align-items: center; /* Center content horizontally */
    text-align: center; /* Center-align text for the container */
    margin-top: 50px;
    width: 100%; /* Ensure container uses full width */
  }

  .question {
    width: 80%; /* Set width of question containers */
    margin-bottom: 40px;
    display: flex; /* Use flexbox to align children */
    flex-direction: column; /* Stack children vertically */
    align-items: center; /* Center-align the question container */
    text-align: left; /* Align text to the left for all child elements */
  }

  .option, label {
    display: flex; /* Using flex to align label and radio button */
    align-items: center; /* Align items in the middle vertically */
    width: 100%; /* Full width to help with alignment */
    margin: 10px 0; /* Spacing for clarity */
    text-align: left; /* Ensure text is aligned to the left */
    justify-content: flex-start; /* Align content to the start (left) of the flex container */
  }

  input[type="radio"] {
    margin-right: 10px; /* Space between radio button and text */
  }

  /* Add a wrapper for labels to control their max width and centering */
  .labels-wrapper {
    display: flex;
    flex-direction: column;
    align-items: flex-start; /* Aligns labels to the left */
    justify-content: center; /* Center aligns the wrapper itself */
    width: fit-content; /* Minimize width to content and allow for centering */
    margin: 0 auto; /* Centers the wrapper in the question container */
  }

  button {
    background-color: #007BFF;
    color: white;
    border: none;
    padding: 10px 20px;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.2s;
    outline: none;
  }

  button:hover {
    background-color: #0056b3;
  }

  button:active {
    transform: scale(0.98);
  }

  button:focus {
    box-shadow: 0 0 0 2px rgba(0,123,255,0.5);
  }
</style>

<div class="container">
  <h1>Quiz Time!</h1>
  <div class="question">
    <p class="body-text">True or False: In a normal distribution, the mean, median, and mode all have the same value and the graph of the distribution is symmetric.</p>
    <div class="labels-wrapper">
      <label class="option">
        <input type="radio" bind:group={answer1} value="true"> True
      </label>
      <label class="option">
        <input type="radio" bind:group={answer1} value="false"> False
      </label>
    </div>
  </div>
  
  <div class="question">
    <p class="body-text">What 2 population parameters determine the shape of the normal curve?</p>
    <div class="labels-wrapper">
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
  </div>
  
  <div class="question">
    <p class="body-text">Which of the following distributions is the least likely to fit a normal distribution?</p>
    <div class="labels-wrapper">
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
        <input type="radio" bind:group={answer3} value="d"> d, distribution of the ages of automobiles in driveable condition
      </label>
      <label class="option">
        <input type="radio" bind:group={answer3} value="e"> e, distribution of the points scored by a basketball player per game
      </label>
    </div>
  </div>
  
  <div class="question">
    <p class="body-text">True or False: The point where the tails of a normal curve reach the x-axis is the exact point where the upper and lower extremes of the population are located.</p>
    <div class="labels-wrapper">
      <label class="option">
        <input type="radio" bind:group={answer4} value="true"> True
      </label>
      <label class="option">
        <input type="radio" bind:group={answer4} value="false"> False
      </label>
    </div>
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
