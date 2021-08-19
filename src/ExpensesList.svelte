<script>
    import Title from './Title.svelte';
    import SingeExpense from './SingleExpense.svelte';
    export let expenses = [];
    export let removeExpense;
</script>

<section>
    <Title title="expense list" />
    <ul>
        {#each expenses as expense}
            <SingeExpense {...expense} {removeExpense} />
        {:else}
            <h2>Currently you have no expenses</h2>
        {/each}
    </ul>
</section>

<style>
    h2 {
        text-transform: capitalize;
    }
</style>
