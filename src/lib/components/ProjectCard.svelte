<script lang="ts">
	export let title: string;
	export let description: string;
	export let tags: string[] = [];
	export let link: string = '#';
	export let color: 'teal' | 'purple' | 'blue' = 'teal';

	const colorClasses = {
		teal: 'group-hover:shadow-[0_0_30px_rgba(45,212,191,0.2)] group-hover:border-neon-teal/50',
		purple: 'group-hover:shadow-[0_0_30px_rgba(139,92,246,0.2)] group-hover:border-neon-purple/50',
		blue: 'group-hover:shadow-[0_0_30px_rgba(14,165,233,0.2)] group-hover:border-neon-blue/50'
	};

	const tagColors = {
		teal: 'text-neon-teal border-neon-teal/20 bg-neon-teal/5',
		purple: 'text-neon-purple border-neon-purple/20 bg-neon-purple/5',
		blue: 'text-neon-blue border-neon-blue/20 bg-neon-blue/5'
	};
</script>

<a href={link} class="group relative block transition-all duration-300 hover:-translate-y-2">
	<div
		class="glass-panel flex h-full flex-col items-start p-8 transition-all duration-300 {colorClasses[
			color
		]}"
	>
		<!-- Icon/Header -->
		<div
			class="mb-6 flex h-12 w-12 items-center justify-center rounded-lg border border-white/10 bg-white/5 transition-transform duration-300 group-hover:scale-110"
		>
			<slot name="icon">
				<div class="h-6 w-6 rounded-sm bg-slate-500"></div>
			</slot>
		</div>

		<h3 class="mb-3 text-xl font-bold transition-colors group-hover:text-white">{title}</h3>

		<p class="mb-6 flex-grow text-sm leading-relaxed text-slate-400">
			{description}
		</p>

		<!-- Tags -->
		<div class="mt-auto flex flex-wrap gap-2">
			{#each tags as tag}
				<span class="rounded border px-2 py-1 font-mono text-xs {tagColors[color]}">
					{tag}
				</span>
			{/each}
		</div>
	</div>
</a>
