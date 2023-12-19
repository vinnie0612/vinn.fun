<script lang="ts">
	import { copyText } from 'svelte-copy';
	import { slide } from 'svelte/transition';
	import { Confetti } from 'svelte-confetti';
	import { onMount } from 'svelte';

	let contact_text = 'contact';
	let contact_menu = false;
	let confetti = false;

	const year = new Date().getFullYear();

	let contacts: { [key: string]: string } = {
		email: 'vin@vinn.fun',
		discord: 'nemvince',
		github: 'vinnie0612'
	};

	let quotes: string[] = [
		'svelte is the best thing ever thing ever made',
		'egoism is based as shit',
		'i am him',
		'server load average goes brr',
		'me when i drop the production db',
		'respect all devs except manjaro users',
		'sudo rm -rf / --no-preserve-root',
		'try docker compose building a relationship',
		'powered by marlboro gold 100s',
		'a small amount of delusion is normal',
		'undefined (but is it really?)',
		'birds dont sing'
	];

	let qotd: string = '';

	onMount(() => {
		qotd = quotes[Math.floor(Math.random() * quotes.length)];
	});

	const copy = (contact: string) => {
		copyText(contacts[contact]);
		contact_menu = false;
		contact_text = 'copied!';
		setTimeout(() => {
			contact_text = 'contact';
		}, 1600);
	};
</script>

<head>
	<title>vinn fun</title>
</head>

<nav class="p-1">
	<ul class="text-lg flex flex-row gap-2 mx-1">
		<li>
			<h1 class="text-xl text-violet-500">
				<button
					on:click={() => {
						if (confetti) return;
						confetti = true;
						setTimeout(() => {
							confetti = false;
						}, 2000);
					}}
				>
					vinn.fun
				</button>
			</h1>
		</li>

		<li class="ml-auto flex flex-row gap-2">
			<button
				class="hover:text-violet-500 transition"
				on:click={() => {
					contact_menu = !contact_menu;
					contact_text = contact_menu ? 'close' : 'contact';
				}}
			>
				{contact_text}
			</button>
			{#if contact_menu}
				<ul class="flex flex-row gap-2" transition:slide={{ duration: 300, axis: 'x' }}>
					{#each Object.keys(contacts) as contact}
						<li>
							<button class="hover:text-violet-500 transition" on:click={() => copy(contact)}
								>{contact}</button
							>
						</li>
					{/each}
				</ul>
			{/if}
		</li>
	</ul>
	<hr />
</nav>

<article class="w-full px-1">
	<h1 class="text-xl text-center">
		<button
			class="text-violet-500"
			on:click={() => {
				qotd = quotes[Math.floor(Math.random() * quotes.length)];
			}}>quote</button
		>
		of the day
	</h1>
	<h2 class="text-lg text-center">
		{qotd}
	</h2>
</article>

{#if confetti}
	<div class="absolute top-1/2 left-1/2">
		<Confetti />
	</div>
{/if}

<footer class="mb-1 mt-auto">
	<p class="text-center">
		no &copy; {year} |
		<a class="hover:text-violet-500 transition" href="https://github.com/vinnie0612/vinn.fun"
			>source</a
		>
	</p>
</footer>
