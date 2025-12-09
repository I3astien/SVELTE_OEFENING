<!--
FEEDBACK FOR BAS:

What he did right:
- Used reactive statements ($:) correctly - great improvement from last time!
- Proper discount calculation logic with hasDiscount
- Two-way binding on inputs

What he did wrong:
- Missing increase/decrease buttons for quantity (requirement #4)
- Missing shipping message (challenge requirement #6)
- Missing discount message display (requirement #5)
- Only showing finalText, not the full output format from the example
- Bug on line 8: ternary operator misuse - can't do assignment inside ternary like that
- Didn't prevent quantity from going below 1
- Didn't format currency with € symbol
- Incomplete implementation - only half of the requirements

Concepts he struggled with:
- Reading all requirements thoroughly
- Following the example output format
- Implementing button handlers for increment/decrement
- Using reactive statements for conditional messages

What needs reinforcement in future assignments:
- Read the example output carefully - it shows what's expected
- All numbered requirements are mandatory
- Challenges are also part of the assignment
- Functions for event handlers (increment/decrement)
-->

<script>
  let price = 10
  let quantity = 1

  // Reactive calculations
  $: total = price * quantity
  $: hasDiscount = total > 50
  $: finalPrice = hasDiscount ? total * 0.9 : total

  // Reactive shipping message
  $: shippingMessage = total >= 30
    ? 'Free shipping! ✓'
    : `Add €${(30 - total).toFixed(2)} more for free shipping`

  // Functions for buttons
  function increment() {
    quantity++
  }

  function decrement() {
    if (quantity > 1) {
      quantity--
    }
  }
</script>

<div class="cart">
  <h2>Shopping Cart</h2>

  <div class="item-info">
    <p>Price per item: €{price.toFixed(2)}</p>
    <div class="quantity-control">
      <span>Quantity:</span>
      <button on:click={decrement}>−</button>
      <span class="quantity-value">{quantity}</span>
      <button on:click={increment}>+</button>
    </div>
  </div>

  <div class="summary">
    <p>Subtotal: €{total.toFixed(2)}</p>

    {#if hasDiscount}
      <p class="discount">10% discount applied!</p>
    {/if}

    <p class="shipping">{shippingMessage}</p>

    <p class="total">Total: €{finalPrice.toFixed(2)}</p>
  </div>
</div>

<style lang="scss">
  .cart {
    max-width: 400px;
    margin: 2rem auto;
    padding: 1.5rem;
    border: 1px solid #ddd;
    border-radius: 8px;
    background: #f9f9f9;

    h2 {
      margin-top: 0;
      color: #333;
    }
  }

  .item-info {
    margin-bottom: 1.5rem;

    p {
      margin: 0.5rem 0;
      color: #555;
    }
  }

  .quantity-control {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    margin-top: 1rem;

    button {
      width: 32px;
      height: 32px;
      border: 1px solid #999;
      background: white;
      border-radius: 4px;
      cursor: pointer;
      font-size: 1.2rem;
      display: flex;
      align-items: center;
      justify-content: center;

      &:hover {
        background: #f0f0f0;
      }

      &:active {
        background: #e0e0e0;
      }
    }

    .quantity-value {
      min-width: 30px;
      text-align: center;
      font-weight: bold;
    }
  }

  .summary {
    border-top: 2px solid #ddd;
    padding-top: 1rem;

    p {
      margin: 0.5rem 0;
    }

    .discount {
      color: #ff6b6b;
      font-weight: bold;
    }

    .shipping {
      color: #51cf66;
      font-weight: 500;
    }

    .total {
      font-size: 1.3rem;
      font-weight: bold;
      margin-top: 1rem;
      color: #333;
    }
  }
</style>
