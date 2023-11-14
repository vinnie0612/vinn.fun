<script lang="ts">
	import { copyText } from 'svelte-copy';
	import { slide } from 'svelte/transition';
	import { Confetti } from 'svelte-confetti';

	let contact_text = 'contact';
	let contact_menu = false;
	let confetti = false;

	const year = new Date().getFullYear();

	let contacts: { [key: string]: string } = {
		email: 'vin@vinn.fun',
		discord: 'nemvince',
		github: 'vinnie0612'
	};

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

<div class="container">
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
							}, 2100);
						}}
					>
						vinn.fun
					</button>
				</h1>
			</li>

			<li class="ml-auto flex flex-row gap-2">
				<button
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
								<button on:click={() => copy(contact)}>{contact}</button>
							</li>
						{/each}
					</ul>
				{/if}
			</li>
		</ul>
		<hr />
	</nav>

	<article class="mx-auto max-w-4xl px-1 content">
		<h1 class="text-xl">
			there's supposed to be <span class="text-violet-500">content</span> here
		</h1>
		<p>but guess who's too lazy</p>
		<p>it's me</p>
		<p>maybe i'll add something here later</p>
		<p>maybe not</p>
	</article>

	{#if confetti}
		<div class="absolute top-1/2 left-1/2">
			<Confetti />
		</div>
	{/if}

	<footer class="mb-1">
		<p class="text-center">no &copy; {year}</p>
	</footer>
</div>

<style>
	.container {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	.content {
		flex: 1;
	}

	footer {
		margin-top: auto;
	}
</style>
