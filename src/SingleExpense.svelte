<script>
    import { getContext } from 'svelte';

    // export let expense;
    // let { name, amount } = expense;
    export let id;
    export let name = '';
    export let amount = 0;
    let displayAmount = false;

    const toggleShowAmount = () => {
        displayAmount = !displayAmount;
    };

    const removeExpense = getContext('remove');
    const setModifiedExpense = getContext('modify');
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
        <button
            class="expense-btn edit-btn"
            aria-label="edit expense"
            on:click={() => setModifiedExpense(id)}
        >
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

<style>
    .single-expense {
        display: flex;
        justify-content: space-between;
        text-transform: capitalize;
        align-items: center;
        margin-bottom: 2rem;
        padding: 1.3rem 1rem;
        border-radius: var(--mainBorderRadius);
        background: var(--mainWhite);
        box-shadow: var(--lightShadow);
    }
    .single-expense h2 {
        margin-bottom: 0;
        font-weight: 300;
    }
    .single-expense h4 {
        margin-bottom: 0;
        margin-top: 1rem;
        font-weight: 300;
        color: var(--primaryColor);
    }

    .expense-btn {
        font-size: 1rem;
        background: transparent;
        border: none;
        margin: 0 0.4rem;
        transition: var(--mainTransition);
        cursor: pointer;
    }
    .expense-btn:hover {
        transform: scale(1.2);
    }
    .amount-btn {
        font-size: 1.3rem;
        background: transparent;
        border: none;
        cursor: pointer;
        color: var(--primaryColor);
    }
    .delete-btn {
        color: red;
    }
    .edit-btn {
        color: green;
    }
</style>
