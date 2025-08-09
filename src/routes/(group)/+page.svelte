<script lang="ts">
	import CardComponent from '$lib/CardComponent.svelte';
	import TerminalComponent from '$lib/TerminalComponent.svelte';

	import IconProjectEuler from '$lib/icon_project_euler.svg?raw';
	import IconSvelte from '$lib/icon_svelte.svg?raw';
	import IconNextcloud from '$lib/icon_nextcloud.svg?raw';
	import IconWireguard from '$lib/icon_wireguard.svg?raw';
	import IconMinio from '$lib/icon_minio.svg?raw';
	import IconCasaos from '$lib/icon_casaos.svg?raw';
	import IconDesmos from '$lib/icon_desmos.svg?raw';
	import BingoIconComponent from '$lib/BingoIconComponent.svelte';

	type Cards = {
		title: string;
		content: string;
		icon: string;
		href: string;
	}[];

	const cards: Cards = [
		{
			title: 'Sphere Surface Area',
			content:
				'I have spent a very very long time proving the surface of a sphere using only polygons. I ended up using a bunch of trapezoids, and proving what the surface area approaches. This page is my ramblings explaining how I did it.',
			icon: IconDesmos,
			href: '/sphere'
		},
		{
			title: 'Notes App',
			content: 'I have been unhappy with every notes app I have tried. So I made my own.',
			icon: IconSvelte,
			href: 'https://example.com'
		},
		{
			title: 'Project Euler',
			content:
				'Project Euler is a website with a bunch of programming challenges. Solving them is how I learned to program. Here is a page that walks through how to solve a few, as a resource to help learning programming.',
			icon: IconProjectEuler,
			href: '/project-euler'
		},
		{
			title: 'Nextcloud',
			content:
				'I really just use the file sharing stuff, but its a well-featured office and free office suite.',
			icon: IconNextcloud,
			href: 'https://nextcloud.tartarus6.com'
		},
		{
			title: 'Wireguard VPN',
			content:
				"I found a neat web-gui for manging it. It's got a few flaws, but it's pretty okay. A self-hosted VPN is pretty nice.",
			icon: IconWireguard,
			href: 'https://wireguard.tartarus6.com'
		},
		{
			title: 'Minio Server',
			content:
				"A decent S3 server. I'd like to switch to something else (the web interface is really slow), but I haven't found a good alternative yet.",
			icon: IconMinio,
			href: 'https://minio.tartarus6.com'
		},
		{
			title: 'CasaOS',
			content:
				'It was a bit of an ordeal to get it working on fedora, but I managed. Its a really nice looking web-based server manager that lets you install the included docker containers with the push of a button.',
			icon: IconCasaos,
			href: 'https://casaos.tartarus6.com'
		}
	];
</script>

<div class="nav-card mx-auto mb-32 grid grid-cols-1 place-items-center">
	<TerminalComponent title="hi!">
		<p>hello</p>
		<p>my name is Tar!</p>
		<p>im a programmer, and i like to make things</p>
		<p></p>
		<p>isnt this quite the website?</p>
		<p>i made it using SvelteKit and tailwindcss</p>
	</TerminalComponent>
	<TerminalComponent title="website?">
		<p>yeah!</p>
		<p>this website (will be) sort of like a resume for me</p>
		<p></p>
		<p>itll explain cool projects ive done, link to em, and such</p>
	</TerminalComponent>
</div>

<div class="grid w-full grid-cols-1">
	<div class="nav-card">
		<CardComponent
			flipped="false"
			title="Bingo"
			content="Right now, it's just got one board which has catchphrases from someone. But I might add more."
			href="/bingo"
		>
			<BingoIconComponent></BingoIconComponent>
		</CardComponent>
	</div>

	{#each cards as card, i}
		<div class="nav-card {i % 2 === 1 ? '' : 'justify-self-end'}">
			<CardComponent
				flipped={i % 2 === 0 ? 'true' : 'false'}
				title={card.title}
				content={card.content}
				href={card.href}
			>
				{@html card.icon}
			</CardComponent>
		</div>
	{/each}
</div>

<style>
	.nav-card {
		width: min(90%, 60rem);
	}
</style>
