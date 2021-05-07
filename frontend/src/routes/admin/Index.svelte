<script lang="ts">
	import { onMount } from 'svelte'

	const onChangeHeight = () => {
		const aside = document.querySelector('aside')
		const nav = document.querySelector('.nav') as HTMLElement
		const marginTop = aside.offsetHeight / 2 - nav.offsetHeight
		nav.style.marginTop = marginTop + 'px'
	}
	onMount(() => onChangeHeight())

	const changeCurrentPage = (name: string) => {
		current_page = name
		// need to load page information
	}

	let current_page: string
</script>

<svelte:window on:resize="{() => onChangeHeight()}" />
<svelte:head>
	<title>syncapod admin</title>
	<link rel="preconnect" href="https://fonts.gstatic.com" />
	<link
		href="https://fonts.googleapis.com/css2?family=Nunito:wght@200&display=swap"
		rel="stylesheet" />
</svelte:head>

<div class="wrapper">
	<aside class="side-panel">
		<div class="logo-wrapper">
			<h2>
				<a
					href="/admin"
					on:click="{() => changeCurrentPage('home')}">syncapod admin</a>
			</h2>
		</div>
		<ul class="nav">
			<li
				class:current="{current_page == 'podcasts'}"
				on:click="{() => changeCurrentPage('podcasts')}">
				Podcasts
			</li>
			<li
				class:current="{current_page == 'users'}"
				on:click="{() => changeCurrentPage('users')}">
				Users
			</li>
		</ul>
	</aside>

	<main>
		<div class="content-wrapper">
			{#if current_page == 'podcasts'}
				<div class="add-pod-wrapper">
					<input
						class="textbox"
						type="text"
						placeholder="Enter podcast RSS URL..." />
					<button class="button" style="width: 60px;">Add</button>
				</div>
			{:else}<span>&#129044; Click Menu Item</span>{/if}
		</div>
	</main>
</div>

<style>
	.wrapper {
		display: flex;
	}
	aside {
		/* padding: 24px; */
		min-height: 100vh;
		width: 220px;
		text-align: center;
		background: #f6f6f6;
	}
	.logo-wrapper {
		padding-top: 8px;
	}
	a {
		text-decoration: none;
		color: black;
	}
	h2 {
		font-family: 'Nunito', 'Gill Sans', 'Gill Sans MT', Calibri,
			'Trebuchet MS', sans-serif;
		font-weight: 200;
		font-size: 1.7em;
	}
	ul.nav {
		display: block;
		padding: 0;
		list-style: none;
	}
	.current {
		font-weight: bold;
		background: rgba(240, 240, 240, 1);
	}
	li {
		display: block;
		cursor: pointer;
		font-family: 'Roboto', 'Gill Sans', 'Gill Sans MT', Calibri,
			'Trebuchet MS', sans-serif;
		width: 100%;
		padding: 18px 0 18px 0;
	}
	li:hover {
		background: rgba(240, 240, 240, 1);
	}
	main {
		flex-grow: 1;
	}
	.content-wrapper {
		display: block;
		padding: 20px;
		/*justify-content: center;*/
		height: 100%;
		font-family: 'Roboto';
		font-size: 1.5em;
	}
	input.textbox {
		width: 240px;
		height: 30px;
		line-height: 30px;
		border: 1px solid rgba(240, 240, 240, 1);
		vertical-align: middle;
	}
	input:placeholder {
		line-height: 30px;
	}
	::placeholder {
		color: rgba(150, 150, 150, 1);
		line-height: 30px;
	}
	button {
		height: 30px;
		line-height: 30px;
		vertical-align: middle;
	}
</style>
