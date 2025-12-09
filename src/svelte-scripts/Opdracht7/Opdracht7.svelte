<script>
  let price = 10
  let quantity = 1
  $: totalPrice = price * quantity
  $: hasDiscount = totalPrice > 50
  $: finalPrice = hasDiscount ? totalPrice * 0.9 : totalPrice
  $: finalText = finalPrice > 0 ? `${finalPrice.toFixed(2)}` : (finalPrice = 0)
</script>

<p>{finalText}</p>

<div class="wrapper">
  <div class="price-quantity">
    <input type="text" bind:value={price} />
    <input type="text" bind:value={quantity} />
  </div>
</div>

<style lang="scss"></style>
