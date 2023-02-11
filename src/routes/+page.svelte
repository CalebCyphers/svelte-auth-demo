<script>
    import { onMount } from "svelte";
    import auth from "../authService";
    import { isAuthenticated, user } from '../store';

    let auth0Client;

    onMount(async () => {
        auth0Client = await auth.createClient();
        isAuthenticated.set(await auth0Client.isAuthenticated());
        user.set(await auth0Client.getUser());
    });

    function login() {
        auth.loginWithPopup(auth0Client);
    }

    function logout() {
        auth.logout(auth0Client);
    }
</script>

<h1>Hello World!</h1>
<p>
	This is a page built with SvelteKit. It's a single-page app, which means that the page loads
	instantly and runs entirely in the browser.
</p>

<p>
	There is another page at '<code>/gated</code>'. It's a protected route, which means that you need to be logged in
	to see it.
</p>

{#if $isAuthenticated}
    <h2>Success!</h2>
    <p>You are logged in as {$user.name}</p>
    <button on:click={logout}>Log out</button>
    
    <a href="/gated">Go to gated page</a>
{:else}
    <p>You are not logged in</p>
    <button on:click={login}>Log in</button>
{/if}

<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to learn more about SvelteKit.</p>
