<script>
    import { blur, fade, fly } from 'svelte/transition';
    import { quintOut } from 'svelte/easing';
</script>

<div class="modal-container" in:blur out:fade>
    <div
        class="modal-content"
        in:fly={{
            y: 200,
            easing: quintOut,
        }}
    >
        <slot />
    </div>
</div>

<style>
    .modal-container {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: rgba(0, 0, 0, 0.7);
        z-index: 2;
    }
    .modal-content {
        background: var(--mainWhite);
        width: 85vw;
        max-width: 35rem;
        margin: 0 auto;
        margin-top: 5rem;
        padding: 3rem;
        border-radius: var(--mainBorderRadius);
        position: relative;
    }
</style>
