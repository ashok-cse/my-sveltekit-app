<script>
    import { page } from '$app/stores';
    console.log($page.params)
</script>

<!-- Language: svelte -->

<div>
    <h1>{$page.params.slug}</h1>
    <h2>{$page.params.slug} : Page</h2>
</div>








