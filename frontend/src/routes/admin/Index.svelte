<script lang="ts">
	import AdminLayout from '../../layout/AdminLayout.svelte'
	import { onMount } from 'svelte'

	const onChangeHeight = () => {
		const aside = document.querySelector('aside')
		const nav = document.querySelector('.nav') as HTMLElement
		const marginTop = aside.offsetHeight / 2 - nav.offsetHeight
		nav.style.marginTop = marginTop + 'px'
	}
	onMount(() => onChangeHeight())

	const changeCurrentPage = (name: string) => {
		console.log('changing page')
		current_page = name
	}

	let current_page: string
</script>

<svelte:window on:resize="{() => onChangeHeight()}" />
<svelte:head>
	<title>syncapod admin</title>
</svelte:head>

<div class="wrapper">
	<aside class="side-panel">
		<h2>
			<a
				href="/admin"
				on:click="{() => changeCurrentPage('home')}">syncapod admin</a>
		</h2>
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
			<span>&#129044; Click Menu Item</span>
		</div>
	</main>
</div>

<style>
	aside {
		/* padding: 24px; */
		min-height: 100vh;
		width: 220px;
		text-align: center;
		background: #f6f6f6;
	}
	a {
		text-decoration: none;
		color: black;
	}
	h2 {
		margin-top: 24px;
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
	.content-wrapper {
		display: flex;
		flex-direction: column;
		justify-content: center;
		text-align: center;
		height: 100%;
		width: 100%;
		font-family: 'Roboto';
		font-size: 1.5em;
	}
</style>
