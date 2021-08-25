<script>
    import { getContext } from 'svelte';
    import { fly } from 'svelte/transition';
    import { flip } from 'svelte/animate';

    import Title from './Title.svelte';
    import SingeExpense from './SingleExpense.svelte';
    export let expenses = [];

    const clearList = getContext('clear');
</script>

<section>
    <Title title="expense list" />
    <ul>
        {#each expenses as expense, index (expense.id)}
            <li
                in:fly={{ x: 200, delay: (index + 1) * 700 }}
                out:fly={{ x: -200 }}
                animate:flip
            >
                <SingeExpense {...expense} />
            </li>
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
