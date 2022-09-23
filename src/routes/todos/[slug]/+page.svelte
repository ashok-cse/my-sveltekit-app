<svelte:head>
    <title>Edit Quiz</title>
    <meta name="description" content="Edit Quiz app" />

</svelte:head>

<script>
    import { page } from '$app/stores';


    console.log($page.params)

</script>


<div>
    <h1>{$page.params.slug}</h1>
    <h2>{$page.params.slug} : Page</h2>
</div>