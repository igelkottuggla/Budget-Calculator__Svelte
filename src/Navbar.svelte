<script>
    export let showForm;
</script>

<nav class="nav">
    <div class="nav-center">
        <h1 class="nav-title">Budget calculator</h1>
        <button type="button" class="nav-btn" on:click={showForm}>
            <i class="far fa-plus-square" />
            add item
        </button>
    </div>
</nav>

<style>
    .nav {
        background: var(--primaryColor);
        height: 5rem;
        display: flex;
        align-items: center;
        box-shadow: var(--lightShadow);
    }

    .nav-center {
        width: 85%;
        max-width: 35rem;
        margin: 0 auto;
        display: flex;
        justify-content: space-between;
    }
    .nav-title {
        text-transform: capitalize;
        color: var(--mainWhite);
        margin-bottom: 0;
        letter-spacing: 2px;
    }
    .nav-btn {
        background: transparent;
        font-size: 1.3rem;
        border: none;
        cursor: pointer;
        text-transform: capitalize;
        transition: var(--mainTransition);
    }
    .nav-btn:hover {
        color: var(--darkGrey);
    }
</style>
