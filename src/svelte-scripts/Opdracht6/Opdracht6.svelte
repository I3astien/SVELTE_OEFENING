<script>
  let fahrenheitInput
  let celciusInput

  let fahrenheitOutput
  let celciusOuput

  let warningMessage = ''

  function temperatureMidstep() {
    if (fahrenheitOutput || celciusOuput) {
      fahrenheitOutput = ''
      celciusOuput = ''
      temperatureOutput()
    } else temperatureOutput()
  }

  function temperatureOutput() {
    if (!fahrenheitInput && !celciusInput) {
      return
    }
    if (fahrenheitInput && celciusInput) {
      warningMessage = 'Only 1 input at a time!'
    }

    if (celciusInput) {
      fahrenheitOutput = (celciusInput * 9) / 5 + 32
    } else celciusOuput = ((fahrenheitInput - 32) * 5) / 9
  }
</script>

<div class="wrapper">
  <div class="input-item">
    <p>Input Fahrenheit here:</p>
    <input type="text" bind:value={fahrenheitInput} />
  </div>
  <div class="input-item">
    <p>Input Celcius here:</p>
    <input type="text" bind:value={celciusInput} />
  </div>
  <button on:click={temperatureMidstep}>Calculate!</button>
</div>

{#if fahrenheitOutput}
  <p>{fahrenheitOutput}</p>{/if}

{#if celciusOuput}
  <p
    style="color: {celciusOuput > 25
      ? 'orange'
      : celciusOuput < 15
        ? 'blue'
        : 'white'}"
  >
    {celciusOuput}
  </p>{/if}

{#if warningMessage}
  <p>{warningMessage}</p>
{:else}{/if}

<style lang="scss">
  .wrapper {
    display: flex;
    justify-content: center;
    gap: 3rem;
  }
</style>
