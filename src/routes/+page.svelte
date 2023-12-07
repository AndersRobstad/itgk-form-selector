<script lang="ts">
	import { onMount } from 'svelte';
	import { slide } from 'svelte/transition';
	import meme from './shinyMeme.jpg';
	import snurrix from './snurrix.gif';

	type Link = {
		name: string;
		href: string;
	};

	const QUESTIONNAIRE_LINKS: Link[] = [
		{ name: 'Spørsmålssett 1', href: 'https://forms.gle/afEtuJFsyGH1PvH37' },
		{ name: 'Spørsmålssett 2', href: 'https://forms.gle/afEtuJFsyGH1PvH37' },
		{ name: 'Spørsmålssett 3', href: 'https://forms.gle/LcKXsQu5wMwPQphQ6' },
		{ name: 'Spørsmålssett 4', href: 'https://forms.gle/No4JW7a6rGgLQ6yc6' },
		{ name: 'Spørsmålssett 5', href: 'https://forms.gle/FEXVpxQNp7hLNF648' }
	];

	let showAllQuestionnaires = false;

	function getRandomQuestionnaire() {
		return QUESTIONNAIRE_LINKS[Math.floor(Math.random() * QUESTIONNAIRE_LINKS.length)];
	}

	function toggleShowAllQuestionnaires() {
		showAllQuestionnaires = !showAllQuestionnaires;
	}
	let randomQuestionnaire: Link | undefined;

	onMount(() => {
		randomQuestionnaire = getRandomQuestionnaire();
	});
</script>

<header class="h-[10vh] py-8 text-center flex flex-col gap-2 border-b border-b-gray-700">
	<h1 class="scroll-m-20 text-3xl font-extrabold tracking-tight">
		ITGK (4109 og 4110) eksamensspørsmål
	</h1>
</header>
<main
	class="px-12 py-10 flex flex-row h-[90vh] max-md:flex-col max-md:items-center max-md:gap-10"
	class:justify-center={randomQuestionnaire === undefined}
>
	{#if randomQuestionnaire}
		<div class="flex flex-col items-center gap-14 w-3/5">
			<div class="flex flex-col gap-4 text-center">
				<div class="flex flex-col gap-2">
					<p class="text-xl font-bold">Robin og Anders foreslår denne:</p>
					<div>
						<a
							href={randomQuestionnaire.href}
							target="_blank"
							rel="noopener noreferrer"
							class="text-xl font-semibold underline hover:text-blue-600 text-red-500"
						>
							{randomQuestionnaire.name}
						</a>
					</div>
				</div>
				<div>
					<button
						class="bg-gray-800 text-white rounded-md py-2 px-2 hover:brightness-90"
						on:click={() => (randomQuestionnaire = getRandomQuestionnaire())}>Få ny quiz</button
					>
				</div>
			</div>
			<div class="border border-gray-500 w-1/2" />
			<div class="flex flex-col gap-4">
				<div class="flex flex-col gap-2">
					<button
						class="text-lg font-semibold flex gap-2 items-center hover:underline"
						on:click={toggleShowAllQuestionnaires}
					>
						Vis alle quizzer
						<input class="cursor-pointer" type="checkbox" checked={showAllQuestionnaires} />
					</button>
				</div>
				{#if showAllQuestionnaires}
					<div class="flex flex-col gap-2" transition:slide>
						{#each QUESTIONNAIRE_LINKS as { name, href }}
							<a
								{href}
								target="_blank"
								rel="noopener noreferrer"
								class="text-lg font-semibold underline hover:text-blue-600"
							>
								{name}
							</a>
						{/each}
					</div>
				{/if}
			</div>
		</div>
		<img src={meme} class="!h-[400px] mix-blend-multiply" alt="" />
	{:else}
		<div
			class="animate-pulse rounded-md bg-gray-300 w-4/5 h-[400px] rounded-full"
			style:display="inline-block"
			style:border-radius="5px"
		/>
	{/if}
	<img src={snurrix} class="h-[20px] mix-blend-multiply absolute top-0 right-0" alt="snurrix" />
	<img src={snurrix} class="h-[20px] mix-blend-multiply absolute top-0 left-0" alt="snurrix" />
	<img src={snurrix} class="h-[20px] mix-blend-multiply absolute bottom-0 left-0" alt="snurrix" />
	<img src={snurrix} class="h-[20px] mix-blend-multiply absolute bottom-0 right-0" alt="snurrix" />
</main>
