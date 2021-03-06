<script>
    import { setContext, onMount, afterUpdate } from 'svelte';

    //components
    import Navbar from './Navbar.svelte';
    import ExpensesList from './ExpensesList.svelte';
    import Totals from './Totals.svelte';
    import ExpenseForm from './ExpenseForm.svelte';
    import Modal from './Modal.svelte';

    //variables
    let expenses = [];

    //set editing variables
    let setName = '';
    let setAmount = null;
    let setID = null;

    //toggle form variables
    let isFormOpen = false;
    //reactive
    $: isEditing = setID ? true : false;
    $: total = expenses.reduce((accum, current) => {
        return (accum += current.amount);
    }, 0);

    //functions
    const showForm = () => {
        isFormOpen = true;
    };

    const closeForm = () => {
        isFormOpen = false;
        setName = '';
        setAmount = null;
        setID = null;
    };

    const removeExpense = (id) => {
        expenses = expenses.filter((item) => item.id !== id);
    };

    const clearList = () => {
        expenses = [];
    };

    const addExpense = ({ name, amount }) => {
        let expense = { id: Math.random() * Date.now(), name, amount };
        expenses = [expense, ...expenses];
        closeForm();
    };

    const setModifiedExpense = (id) => {
        let expense = expenses.find((item) => item.id === id);
        setID = expense.id;
        setName = expense.name;
        setAmount = expense.amount;
        showForm();
    };

    const editExpense = ({ name, amount }) => {
        expenses = expenses.map((expense) => {
            return expense.id === setID
                ? { ...expense, name, amount }
                : { ...expense };
        });

        closeForm();
    };

    //context
    setContext('remove', removeExpense);
    setContext('clear', clearList);
    setContext('modify', setModifiedExpense);

    //local storage
    const setLocalStorage = () => {
        localStorage.setItem('expenses', JSON.stringify(expenses));
    };

    onMount(() => {
        expenses = localStorage.getItem('expenses')
            ? JSON.parse(localStorage.getItem('expenses'))
            : [];
    });

    afterUpdate(() => {
        setLocalStorage();
    });
</script>

<Navbar {showForm} />
<main class="content">
    {#if isFormOpen}
        <Modal>
            <ExpenseForm
                {addExpense}
                name={setName}
                amount={setAmount}
                {isEditing}
                {editExpense}
                {closeForm}
            />
        </Modal>
    {/if}
    <Totals title="Total expenses" {total} />
    <ExpensesList {expenses} />
</main>

<style>
    .content {
        padding: 3rem 0;
        width: 85vw;
        max-width: 35rem;
        margin: 0 auto;
    }
</style>
