<script>
  import { questions } from '../heartburn.json';
  import { outcomes } from '../heartburn.json';
  import Icon from '@iconify/svelte';
  
  // --- VARIABLES ---
  // Start settings variables
  let currentQuestionId = questions[0].id;
  let isDisabled = true;
  let showForm = true;

   // Current questions variables
  let currentQuestionObject = {};
  currentQuestionObject = questions.find((options) => options.id == currentQuestionId);
  let selectedOptionId = '';
  let nextQuestionArray;

  // User score variable
  let userScore = 0;

  // Outcomes variables
  let outcomeId = '';
  let outcomeObject = {};


  // --- FUNCTIONS ---
  function clickOnNextButtonHandler() {
    addScoreToUserScore();
    getNextAction();
    isDisabled = true;
  }

  function getNextAction() {

    if ( currentQuestionObject.next.find((next) => next.answered !== undefined) ) {
      nextQuestionArray = currentQuestionObject.next.find((next) => next.answered === selectedOptionId);
    } else if ( currentQuestionObject.next.find((next) => next.next_question !== undefined) ) {
      nextQuestionArray = currentQuestionObject.next[0];
    } else if ( currentQuestionObject.next.find((next) => next.max_score !== undefined) ) {
      showForm = false;
      showOutcome();
      return;
    }
    let nextQuestionId = nextQuestionArray.next_question;
    // Change currentQuestionId to new question
    currentQuestionId = nextQuestionId;
    currentQuestionObject = questions.find((options) => options.id == currentQuestionId);
  }
  function showOutcome() {
      // Hard-coded
      if ( userScore <= 5 ) {
        outcomeId = currentQuestionObject.next[0].outcome;
      } else if ( userScore <= 49 ) {
        outcomeId = currentQuestionObject.next[1].outcome;
      } else {
        outcomeId = currentQuestionObject.next[2].outcome;
      }
      outcomeObject = outcomes.find((outcome) => outcome.id == outcomeId);
  }
  function addScoreToUserScore() {
    let selectedOptionObject = currentQuestionObject.answers.find((answers) => answers.id === selectedOptionId);
    let selectedOptionScore = selectedOptionObject.score;
    userScore = userScore + selectedOptionScore;
  }
</script>

<section>
  {#if showForm }
  <div class="form-wrapper">
    <h2>{currentQuestionObject.question_text}</h2>
    <div class="option-wrapper">
      {#each currentQuestionObject.answers as { id, label }}
        <input
          type="radio"
          name={currentQuestionObject.id}
          id={id}
          value={id}
          bind:group={selectedOptionId}
          on:change={()=>isDisabled = false}
        />
        <label for={id}>{label}</label>
      {/each}
    </div>
  </div>
  <div class="next-button">
    <button disabled={isDisabled} on:click={clickOnNextButtonHandler}>
      <div>
        <div class="button-text">Next</div>
        <Icon icon="material-symbols:arrow-circle-right-outline-rounded" width="2rem"/>
      </div>
    </button>
  </div>
 {:else}
  <div class="outcome-wrapper">
    <div class="content">
      <h2>Thank you for answering the questions!</h2>
      <p>{outcomeObject.text}</p>
      {#if outcomeObject.show_booking_button}
      <button>
        <div>
          <div class="button-text">Book a meeting</div>
          <Icon icon="material-symbols:arrow-circle-right-outline-rounded" width="2rem"/>
        </div>
      </button>
      {/if}
    </div>
    <a href="." style="text-align: center">Back to start screen</a>
  </div>
 {/if}
</section>

<style>
  section {
    height: 100%;
    display: flex;
    flex: 1;
    flex-direction: column;
    align-items: flex-end;
    justify-content: end;
  }
  .option-wrapper {
    display: flex;
    align-items: center;
  }
  .outcome-wrapper {
    display: flex;
    flex: 1;
    flex-direction: column;
    justify-content: space-between;
  }
  label {
    background-color: var(--blue-600);
    transition: background-color 250ms;
    color: var(--white-100);
    border-radius: 6.25rem;
    box-shadow: 0px 2px 4px 0px rgba(0, 27, 46, 0.24);
    padding: 1rem 2rem;
    color: var(--white-100);
    text-align: center;
    font-size: 1rem;
    font-style: normal;
    font-weight: 600;
    line-height: normal;
    letter-spacing: 0.07rem;
    text-transform: uppercase;
    margin-right: calc(var(--grid-base) * 2);
  }
  label:hover {
    background-color: var(--blue-500);
  }
  input:checked + label {
    background-color: var(--blue-400);
  }
  .next-button {
    margin-top: calc(var(--grid-base) * 6);
  }
  button {
    background-color: var(--blue-600);
    transition: background-color 250ms;
    border: none;
    border-radius: 6.25rem;
    box-shadow: 0px 2px 4px 0px rgba(0, 27, 46, 0.24);
    height: 3rem;
    padding: 0.75rem 1rem 0.75rem 1.5rem;
    color: var(--white-100);
    text-align: center;
    font-size: 1rem;
    font-weight: 600;
    letter-spacing: 0.07rem;
    text-transform: uppercase;
    display: flex;
    align-items: center;
  }
  button > div {
    display: flex;
    align-items: center;
  }
  .button-text {
    margin-right: var(--grid-base);
  }
  button:hover {
    background-color: var(--blue-500);
  }
  button:disabled {
    background-color: #2A4A60;
    color: #AAC6C4;
  }
</style>
