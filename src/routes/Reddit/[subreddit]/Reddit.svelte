<script>
    export let data;

    function truncate(text, length) {
        return text.length > length ? text.substring(0, length) + "..." : text;
    }
</script>

<svelte:head>
	<title>reddit: {data.subreddit}</title>
</svelte:head>

<div class="container">
    {#each data.posts as post}  
        <!-- {@debug post} -->
        <div class="post">
            <div class="post-content">
                <h2 class="post-title"><a href="https://reddit.com{post.permalink}" target="_blank">{post.title}</a></h2>
                <div class="post-text">{truncate(post.selftext, 100)}</div>
                <div class="post-stats">🔼 {post.ups} | 💬 {post.num_comments}</div>
            </div>
            {#if post.thumbnail && post.thumbnail !== "self" && post.thumbnail !== "default"}
                <img src={post.thumbnail} alt="Post thumbnail" class="post-thumbnail" />
            {/if}
        </div>
    {/each}
</div>

<style>
    .container {
        max-width: 800px;
        margin: 0 auto;
    }
    .post {
        display: flex;
        min-height: 5em;
        padding: 5px;
    }
    .post-title {
        margin-bottom: 10px;
        color: black;
    }
    .post-stats {
        font-size: 0.9em;
        color: #888;
    }
    .post-content {
        flex: 1;
        display: flex;
        flex-direction: column;
    }
    .post-text {
        flex-grow: 1;
    }
    .post-thumbnail {
        margin-left: 10px;
        max-height: 5rem;
    }
</style>