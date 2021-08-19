<script>
    // export let expense;
    // let { name, amount } = expense;
    export let id;
    export let name = '';
    export let amount = 0;
    let displayAmount = false;
    export let removeExpense;

    const toggleShowAmount = () => {
        displayAmount = !displayAmount;
    };
</script>

<article class="single-expense">
    <div class="expense-info">
        <h2>
            {name}
            <button
                class="amount-btn"
                aria-label="show more"
                on:click={toggleShowAmount}
            >
                <i class="fas fa-caret-down" />
            </button>
        </h2>
        {#if displayAmount}
            <h4>amount: ${amount}</h4>
        {/if}
    </div>
    <div class="expense-buttons">
        <button class="expense-btn edit-btn" aria-label="edit expense">
            <i class="fas fa-pen" />
        </button>
        <button
            class="expense-btn delete-btn"
            aria-label="delete expense"
            on:click={() => removeExpense(id)}
        >
            <i class="fas fa-trash" />
        </button>
    </div>
</article>
