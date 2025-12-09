<!--
FEEDBACK FOR BAS:

What he did well:
- Conversion formulas are correct
- Good nested ternary operator for color challenge
- Tried to add validation (warning message)

What he did wrong:
- COMPLETELY MISSED THE MAIN CONCEPT: didn't use reactive statements ($:) at all!
- Created manual functions and a button instead of automatic reactivity
- Overly complex with temperatureMidstep and temperatureOutput functions
- Created separate input/output variables when only need one variable per temperature
- Assignment said "automatically updates" but his requires button click
- Missing .toFixed(1) for decimal formatting
- Empty {:else} block on line 61
- Typo: "Celcius" should be "Celsius"

Concepts he struggled with:
- Understanding what reactive statements ($:) are and how they work
- Reading the assignment (it said "automatically updates", not "button to calculate")
- The core concept of this entire assignment (reactive statements!)
- Svelte's reactivity model

What needs reinforcement in future assignments:
- Reactive statements ($:) - CRITICAL concept in Svelte
- Understanding that $: runs automatically when dependencies change
- Reading requirements carefully (missed the whole point!)
- Keep solutions simple - don't over-engineer
-->

<script>
  // We only bind to celsius, and calculate fahrenheit from it
  let celsius = 20

  // Reactive statement - automatically updates when celsius changes
  $: fahrenheit = Number(((celsius * 9/5) + 32).toFixed(1))

  // Reactive statement for computed value (color based on celsius)
  $: temperatureColor = celsius < 15 ? 'lightblue' : celsius > 25 ? 'orange' : 'white'

  // Reactive statement for status message
  $: temperatureStatus = celsius < 15 ? 'Cold ❄️' : celsius > 25 ? 'Hot 🔥' : 'Comfortable ✨'
</script>

<div class="container" style="background-color: {temperatureColor}">
  <h2>Temperature Converter</h2>

  <div class="input-group">
    <label>
      Celsius:
      <input
        type="number"
        bind:value={celsius}
        step="0.1"
      />
      °C
    </label>
  </div>

  <div class="input-group">
    <label>
      Fahrenheit:
      <input
        type="number"
        value={fahrenheit}
        readonly
      />
      °F
    </label>
  </div>

  <p class="status">Current temp: {temperatureStatus}</p>
</div>

<style lang="scss">
  .container {
    padding: 2rem;
    max-width: 400px;
    margin: 2rem auto;
    border-radius: 8px;
    transition: background-color 0.3s ease;
  }

  h2 {
    color: #333;
    text-align: center;
    margin-bottom: 1.5rem;
  }

  .input-group {
    margin-bottom: 1rem;

    label {
      display: flex;
      align-items: center;
      gap: 0.5rem;
      color: #333;
      font-weight: 500;

      input {
        flex: 1;
        padding: 0.5rem;
        border: 2px solid rgba(0, 0, 0, 0.2);
        border-radius: 4px;
        font-size: 1rem;

        &:focus {
          outline: none;
          border-color: rgb(48, 86, 48);
        }
      }
    }
  }

  .status {
    text-align: center;
    margin-top: 1.5rem;
    font-size: 1.2rem;
    font-weight: bold;
    color: #333;
  }
</style>
