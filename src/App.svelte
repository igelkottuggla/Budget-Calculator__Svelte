<script>
    import { setContext } from 'svelte';

    //components
    import Navbar from './Navbar.svelte';
    import ExpensesList from './ExpensesList.svelte';
    import Totals from './Totals.svelte';
    import ExpenseForm from './ExpenseForm.svelte';

    //data
    import expensesData from './expenses';

    //variables
    let expenses = [...expensesData];

    //reactive
    $: total = expenses.reduce((accum, current) => {
        return (accum += current.amount);
    }, 0);

    //functions
    const removeExpense = (id) => {
        expenses = expenses.filter((item) => item.id !== id);
    };

    const clearList = () => {
        expenses = [];
    };

    //context
    setContext('remove', removeExpense);
    setContext('clear', clearList);
</script>

<Navbar />
<main class="content">
    <ExpenseForm />
    <Totals title="Total expenses" {total} />
    <ExpensesList {expenses} />
</main>
