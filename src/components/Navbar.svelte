<script>

    import { isFullScreen } from '../stores/player';

    import CloseFullScreenButton from './CloseFullScreenButton.svelte'

    let isActive = false;

</script>

<nav class="navbar">
    <div class="navbar-brand">
        <a href="#!" class="navbar-burger burger" class:is-active={isActive} on:click|preventDefault={() => isActive = !isActive }>
            <span></span>
            <span></span>
            <span></span>
        </a>
    </div>
    <div class="navbar-menu" class:is-active={isActive}>
        <div class="navbar-start">
            <a href="/karaom" class="navbar-item">Home</a>
            {#if $isFullScreen}
                <div class="navbar-item">
                    <CloseFullScreenButton />
                </div>
            {/if}
        </div>
        <div class="navbar-end">
            <div class="navbar-item">
                <div class="buttons">
                    <a href="https://github.com/Karaom/karaom-public/issues/new?title=I%20have%20a%20problem%20with%20Karaom&body=**Explain%20what%20is%20wrong:**%20" target="_blank" class="button is-primary">A problem?</a>
                    <a href="https://github.com/Karaom/karaom" target="_blank" class="button is-dark"><i class="fab fa-github"></i></a>
                </div>
            </div>
        </div>
    </div>
</nav>