<script>
    import { getContext } from 'svelte';

    import Title from './Title.svelte';
    import SingeExpense from './SingleExpense.svelte';
    export let expenses = [];

    const clearList = getContext('clear');
</script>

<section>
    <Title title="expense list" />
    <ul>
        {#each expenses as expense}
            <SingeExpense {...expense} />
        {:else}
            <h2>No expenses added to the list</h2>
        {/each}
    </ul>
    {#if expenses.length > 0}
        <button
            type="button"
            class="btn btn-primary btn-block"
            on:click={clearList}
        >
            clear expenses
        </button>
    {/if}
</section>

<style>
    h2 {
        text-transform: capitalize;
    }
</style>
