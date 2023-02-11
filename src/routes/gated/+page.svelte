<script>
    import { goto } from '$app/navigation';
    import { isAuthenticated } from '$app/stores';

    $: if (!isAuthenticated) goto('/')
</script>

<h1>Gated Page</h1>

<p>You should not be able to see this page unless you are logged in!</p>

<button on:click={goto('/')}>Return to homepage</button>