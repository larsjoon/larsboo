<script lang="ts">
	import { onMount } from 'svelte';
	import ProjectCard from '$lib/components/ProjectCard.svelte';
	import LorenzAttractor from '$lib/components/LorenzAttractor.svelte';

	let mounted = false;
	let text = '';
	// The roles to cycle through
	const phrases = [
		'Mathematics & Data',
		'Creative Development',
		'Machine Learning',
		'Interactive Design'
	];
	let phraseIndex = 0;
	let charIndex = 0;
	let isDeleting = false;

	// Typing configuration
	const typeSpeed = 100;
	const deleteSpeed = 50;
	const pauseEnd = 2000;

	function type() {
		const currentPhrase = phrases[phraseIndex];

		if (isDeleting) {
			text = currentPhrase.substring(0, charIndex - 1);
			charIndex--;
		} else {
			text = currentPhrase.substring(0, charIndex + 1);
			charIndex++;
		}

		let delta = isDeleting ? deleteSpeed : typeSpeed;

		if (!isDeleting && charIndex === currentPhrase.length) {
			isDeleting = true;
			delta = pauseEnd;
		} else if (isDeleting && charIndex === 0) {
			isDeleting = false;
			phraseIndex = (phraseIndex + 1) % phrases.length;
			delta = 500;
		}

		setTimeout(type, delta);
	}

	onMount(() => {
		mounted = true;
		setTimeout(type, 1000); // Start typing after initial load
	});
</script>

<!-- Hero Section -->
<section
	class="relative flex min-h-[90vh] flex-col items-center justify-center overflow-hidden px-6 text-center"
>
	<div class="bg-radial-gradient absolute inset-0 z-0 opacity-30"></div>

	<div class="z-10 mx-auto max-w-4xl space-y-6">
		<div
			class="mb-4 inline-block animate-[fadeIn_0.5s_ease-out] rounded-full border border-neon-teal/20 bg-neon-teal/5 px-3 py-1 font-mono text-xs text-neon-teal backdrop-blur-sm"
		>
			22 Y/O • THE NETHERLANDS
		</div>

		<h1 class="mb-2 text-5xl font-bold tracking-tight md:text-7xl lg:text-8xl">
			<span class="block animate-[slideUp_0.8s_ease-out] text-white">Lars Vlasveld</span>
			<span
				class="text-gradient mt-2 block min-h-[1.2em] animate-[slideUp_1s_ease-out_0.2s_both] text-3xl font-light md:text-5xl"
			>
				{text}<span class="animate-[glitch_1s_linear_infinite] opacity-70">_</span>
			</span>
		</h1>

		<p
			class="mx-auto max-w-2xl animate-[slideUp_1s_ease-out_0.4s_both] text-lg leading-relaxed text-slate-400 md:text-xl"
		>
			Crafting elegant solutions at the intersection of applied mathematics and modern data science.
			Building digital experiences that are as logical as they are beautiful.
		</p>

		<div
			class="flex animate-[slideUp_1s_ease-out_0.6s_both] flex-col items-center justify-center gap-4 pt-8 sm:flex-row"
		>
			<a href="#projects" class="btn-primary min-w-[160px]"> View Projects </a>
			<a
				href="#contact"
				class="group min-w-[160px] rounded-lg border border-white/20 px-6 py-3 font-mono text-sm transition-all hover:bg-white/5"
			>
				hi@lars.boo <span class="inline-block transition-transform group-hover:translate-x-1"
					>-></span
				>
			</a>
		</div>
	</div>

	<!-- Scroll Indicator -->
	<div
		class="absolute bottom-10 left-1/2 -translate-x-1/2 animate-[float_3s_ease-in-out_infinite] opacity-50"
	>
		<svg
			width="24"
			height="24"
			viewBox="0 0 24 24"
			fill="none"
			stroke="currentColor"
			stroke-width="2"
		>
			<path d="M7 13l5 5 5-5M7 6l5 5 5-5" />
		</svg>
	</div>
</section>

<!-- About Section -->
<section id="about" class="relative px-6 py-32">
	<div class="mx-auto max-w-6xl">
		<div class="grid items-center gap-16 md:grid-cols-2">
			<!-- Stats / Visual -->
			<div class="relative order-2 md:order-1">
				<div class="absolute -inset-4 rounded-full bg-neon-teal/20 opacity-20 blur-3xl"></div>
				<div
					class="glass-panel group relative overflow-hidden p-2 transition-colors duration-500 hover:border-neon-teal/30"
				>
					<LorenzAttractor />
				</div>
			</div>

			<!-- Text Content -->
			<div class="order-1 space-y-6 md:order-2">
				<h2 class="text-3xl font-bold md:text-4xl">
					<span class="mb-2 block font-mono text-lg text-neon-teal">01. ABOUT ME</span>
					Curiosity, Code & Creativity.
				</h2>
				<p class="leading-relaxed text-slate-400">
					My name is Lars, a 22-year-old student who enjoys figuring out how things work and turning
					that curiosity into code. I'm especially interested in AI and crypto, and I like digging
					into how models learn, how systems scale, and how technology shapes the way we interact
					with the world.
				</p>
				<p class="leading-relaxed text-slate-400">
					When I'm not experimenting with ideas or learning something new, I'm building fast,
					accessible web experiences with a strong focus on design and performance—like this site,
					built with <span class="font-bold text-neon-teal">SvelteKit</span>. Outside of tech, I
					spend a lot of time with music, which often sneaks its way into how I think about rhythm,
					structure, and visuals.
				</p>

				<div class="flex flex-wrap gap-3 pt-4">
					{#each ['Python', 'SQL', 'Svelte', 'Java', 'Web Development'] as tech}
						<span
							class="cursor-default rounded-full border border-white/10 bg-white/5 px-3 py-1 font-mono text-sm text-slate-300 transition-colors hover:border-neon-teal/50"
						>
							{tech}
						</span>
					{/each}
				</div>
			</div>
		</div>
	</div>
</section>

<!-- Projects Section -->
<section id="projects" class="relative bg-math-blue/30 px-6 py-32">
	<div class="mx-auto max-w-7xl">
		<div class="mb-16 text-center">
			<span class="mb-4 block font-mono text-sm tracking-widest text-neon-purple">02. WORK</span>
			<h2 class="text-4xl font-bold md:text-5xl">Featured Projects</h2>
		</div>

		<div
			class="glass-panel mx-auto max-w-2xl border-2 border-dashed border-white/10 p-16 text-center"
		>
			<div class="mb-6">
				<svg
					class="mx-auto h-16 w-16 text-neon-purple opacity-50"
					fill="none"
					stroke="currentColor"
					viewBox="0 0 24 24"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						stroke-width="1.5"
						d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z"
					/>
				</svg>
			</div>
			<h3 class="mb-3 text-2xl font-bold text-white">Projects Coming Soon</h3>
			<p class="mx-auto mb-8 max-w-md text-slate-400">
				I'm currently working on some exciting projects in data science and web development. Check
				back soon!
			</p>
			<div class="inline-flex gap-3">
				<div class="h-3 w-3 animate-pulse rounded-full bg-neon-teal"></div>
				<div
					class="h-3 w-3 animate-pulse rounded-full bg-neon-purple"
					style="animation-delay: 0.2s"
				></div>
				<div
					class="h-3 w-3 animate-pulse rounded-full bg-neon-blue"
					style="animation-delay: 0.4s"
				></div>
			</div>
		</div>
	</div>
</section>

<!-- Contact Section -->
<section id="contact" class="relative px-6 py-32">
	<div class="mx-auto max-w-4xl text-center">
		<span class="mb-4 block font-mono text-sm tracking-widest text-neon-teal">03. CONTACT</span>
		<h2 class="mb-6 text-4xl font-bold md:text-5xl">Let's Connect</h2>
		<p class="mx-auto mb-12 max-w-2xl text-lg text-slate-400">
			Interested in collaborating on a project, have a question, or just want to say hi? Feel free
			to reach out!
		</p>

		<a href="mailto:hi@lars.boo" class="btn-primary mb-16 inline-block px-8 py-4 text-lg">
			Get In Touch
		</a>

		<!-- Social Links -->
		<div class="flex justify-center gap-6">
			<a
				href="https://x.com/larsjoon"
				target="_blank"
				rel="noopener noreferrer"
				aria-label="X (Twitter)"
				class="group flex h-14 w-14 items-center justify-center rounded-full border border-white/10 bg-white/5 transition-all duration-300 hover:border-neon-teal/50 hover:bg-neon-teal/10"
			>
				<svg
					class="h-6 w-6 text-slate-400 transition-colors group-hover:text-neon-teal"
					fill="currentColor"
					viewBox="0 0 24 24"
				>
					<path
						d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"
					/>
				</svg>
			</a>

			<a
				href="https://instagram.com/larsjoon"
				target="_blank"
				rel="noopener noreferrer"
				aria-label="Instagram"
				class="group flex h-14 w-14 items-center justify-center rounded-full border border-white/10 bg-white/5 transition-all duration-300 hover:border-neon-purple/50 hover:bg-neon-purple/10"
			>
				<svg
					class="h-6 w-6 text-slate-400 transition-colors group-hover:text-neon-purple"
					fill="currentColor"
					viewBox="0 0 24 24"
				>
					<path
						d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 100 12.324 6.162 6.162 0 000-12.324zM12 16a4 4 0 110-8 4 4 0 010 8zm6.406-11.845a1.44 1.44 0 100 2.881 1.44 1.44 0 000-2.881z"
					/>
				</svg>
			</a>

			<a
				href="https://github.com/larsjoon/"
				target="_blank"
				rel="noopener noreferrer"
				aria-label="GitHub"
				class="group flex h-14 w-14 items-center justify-center rounded-full border border-white/10 bg-white/5 transition-all duration-300 hover:border-white/50 hover:bg-white/10"
			>
				<svg
					class="h-6 w-6 text-slate-400 transition-colors group-hover:text-white"
					fill="currentColor"
					viewBox="0 0 24 24"
				>
					<path
						d="M12 0C5.374 0 0 5.373 0 12c0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23A11.509 11.509 0 0112 5.803c1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576C20.566 21.797 24 17.3 24 12c0-6.627-5.373-12-12-12z"
					/>
				</svg>
			</a>

			<a
				href="https://www.linkedin.com/in/larsvlasveld/"
				target="_blank"
				rel="noopener noreferrer"
				aria-label="LinkedIn"
				class="group flex h-14 w-14 items-center justify-center rounded-full border border-white/10 bg-white/5 transition-all duration-300 hover:border-neon-blue/50 hover:bg-neon-blue/10"
			>
				<svg
					class="h-6 w-6 text-slate-400 transition-colors group-hover:text-neon-blue"
					fill="currentColor"
					viewBox="0 0 24 24"
				>
					<path
						d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"
					/>
				</svg>
			</a>
		</div>
	</div>
</section>
