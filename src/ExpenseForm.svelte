<script>
    import Title from './Title.svelte';
    export let name = '';
    export let amount = null;
    export let addExpense;
    export let isEditing;
    export let editExpense;
    export let closeForm;

    $: isEmpty = !name || !amount;

    const handleSubmit = () => {
        if (isEditing) {
            editExpense({ name, amount });
        } else {
            addExpense({ name, amount });
        }
        name = '';
        amount = null;
    };
</script>

<section class="form">
    <Title title="add expense" />
    <form class="expense-form" on:submit|preventDefault={handleSubmit}>
        <div class="form-control">
            <label for="name">name</label>
            <input type="text" id="name" bind:value={name} />
        </div>
        <div class="form-control">
            <label for="ampount">amount</label>
            <input type="number" id="amount" bind:value={amount} />
        </div>
        {#if isEmpty}
            <p class="form-empty">please, fill out all from fields</p>
        {/if}
        <button
            type="submit"
            class="btn btn-block"
            class:disabled={isEmpty}
            disabled={isEmpty}
        >
            {#if isEditing} edit expense {:else} add expense {/if}
        </button>
        <button type="button" class="close-btn" on:click={closeForm}>
            <i class="fas fa-times" />
            close
        </button>
    </form>
</section>

<style>
    .expense-form {
        background: var(--mainWhite);
        padding: 1.25rem 1rem;
        text-transform: capitalize;
        border-radius: var(--mainBorderRadius);
    }

    .form-control label {
        display: block;
    }
    .form-control input {
        width: 100%;
        border: none;
        border-bottom: 2px solid var(--darkGrey);
        margin-bottom: 1.25rem;
        padding: 0.5rem;
        font-size: 1.2rem;
    }
    .form-empty {
        text-align: center;
        color: red;
    }
    .form {
        position: relative;
    }
    .close-btn {
        position: absolute;
        top: 0;
        right: 0;
        font-size: 1.2rem;
        text-transform: capitalize;
        display: flex;
        align-items: center;
        width: 4.2rem;
        justify-content: space-between;
        background: transparent;
        border: none;
        color: red;
        cursor: pointer;
    }
</style>
