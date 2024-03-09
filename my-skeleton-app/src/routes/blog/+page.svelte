
<script>
    import { onMount } from 'svelte';
    let posts = [];

    onMount(async () => {
        const res = await fetch('/api/blog/posts');
        posts = await res.json();
    });
</script>

<section>
    {#each posts as post (post.id)}
        <article>
            <h2>{post.title}</h2>
            <p>{post.summary}</p>
            <a href="blog/{post.id}">Read more</a>
        </article>
    {/each}
</section></script>