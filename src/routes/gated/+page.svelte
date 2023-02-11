<script>
    import { isAuthenticated } from "../../store";
</script>

{#if $isAuthenticated}
<h1>You can see the gated content!</h1>

<p>You should not be able to see this unless you are logged in!</p>

<a href="/">Return to homepage</a>
{:else}
<h1>Woah there Bucko</h1>
<h2>You are not logged in</h2>
<a href="/">Return to homepage</a> 
<p>You will be logged out automatically</p>
{/if}