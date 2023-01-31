<script>
import Header from '$lib/components/header.svelte'
import Analytics from '$lib/components/analytics.svelte'
</script>

<style>

</style>

<Header />
<Analytics />

<div class="container">
<slot></slot>
</div>
