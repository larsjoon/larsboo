<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import { page } from '$app/stores';
	import { fade } from 'svelte/transition';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<title>Lars Vlasveld | Applied Math & Data Science</title>
	<meta
		name="description"
		content="Portfolio of Lars Vlasveld, an Applied Mathematics and Data Science student based in The Netherlands. Exploring the intersection of logic, code, and design."
	/>
</svelte:head>

<div
	class="relative flex min-h-screen flex-col overflow-hidden selection:bg-neon-teal selection:text-math-dark"
>
	<!-- Background grid effect -->
	<div class="pointer-events-none fixed inset-0 z-0">
		<!-- Primary Grid (Teal) -->
		<div
			class="absolute inset-[-100%] animate-grid-flow opacity-[0.15] will-change-transform"
			style="background-image: radial-gradient(#2dd4bf 1px, transparent 1px); background-size: 40px 40px;"
		></div>

		<!-- Secondary Grid (Purple - Interference Layer) -->
		<div
			class="absolute inset-[-100%] animate-grid-flow-reverse opacity-[0.10] will-change-transform"
			style="background-image: radial-gradient(#8b5cf6 1px, transparent 1px); background-size: 60px 60px;"
		></div>
	</div>

	<nav
		class="fixed z-50 w-full border-b border-white/5 bg-math-dark/80 backdrop-blur-md transition-all duration-300"
	>
		<div class="mx-auto flex h-20 max-w-7xl items-center justify-between px-6">
			<a
				href="/"
				class="font-mono text-2xl font-bold tracking-tighter transition-colors hover:text-neon-teal"
			>
				Lars<span class="text-neon-teal">.</span>boo
			</a>

			<div class="hidden items-center gap-8 font-mono text-sm md:flex">
				<a href="#about" class="transition-colors hover:text-neon-teal">/about</a>
				<a href="#projects" class="transition-colors hover:text-neon-teal">/projects</a>
				<a href="#contact" class="transition-colors hover:text-neon-teal">/contact</a>
				<a href="mailto:hi@lars.boo" class="btn-primary px-4 py-2 shadow-none hover:shadow-lg"
					>Let's Talk</a
				>
			</div>
		</div>
	</nav>

	<main class="z-10 flex-grow pt-20">
		{#key $page.url.pathname}
			<div in:fade={{ duration: 300, delay: 300 }} out:fade={{ duration: 300 }}>
				{@render children()}
			</div>
		{/key}
	</main>

	<footer class="z-10 border-t border-white/10 bg-math-dark">
		<div class="mx-auto max-w-7xl px-6 py-8 text-center">
			<div class="text-sm text-slate-400">
				© {new Date().getFullYear()} Lars Vlasveld. All rights reserved.
			</div>
		</div>
	</footer>
</div>
