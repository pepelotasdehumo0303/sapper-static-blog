<script context="module">
	export function preload() {
		return this.fetch(`blog.json`)
			.then((r) => r.json())
			.then((posts) => {
				return { posts };
			});
	}
</script>

<script>
	export let posts;
</script>

<svelte:head>
	<title>Blog</title>
</svelte:head>

<h1>Recent posts</h1>

<ul>
	<div class="sr-only">
		<!--You can iterate over the links from your preload fetch of posts-->
		{#each posts as { slug, title }}
			<a rel="prefetch" href="blog/{slug}">{title}</a>
		{/each}
		<!--And manually put any links that are breaking as well (it means Sapper doesn't think you're using them)-->
		<a rel="prefetch" href="/someotherpage"
			>Some page name for screen readers (nobody else sees it)</a
		>
	</div>
</ul>

<style>
	ul {
		margin: 0 0 1em 0;
		line-height: 1.5;
	}
	:global(sr-only) {
		clip: rect(0 0 0 0);
		clip-path: inset(100%);
		height: 1px;
		overflow: hidden;
		position: absolute;
		white-space: nowrap;
		width: 1px;
	}
</style>
