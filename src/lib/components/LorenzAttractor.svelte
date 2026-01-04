<script lang="ts">
	import { onMount } from 'svelte';

	let canvas: HTMLCanvasElement;
	let width: number;
	let height: number;

	onMount(() => {
		const ctx = canvas.getContext('2d');
		if (!ctx) return;

		// Lorenz System Parameters
		const sigma = 10;
		const rho = 28;
		const beta = 8 / 3;

		// Start closer to the attractor's "sweet spot" for faster visual
		let x = 1;
		let y = 1;
		let z = 1;

		// Time step
		const dt = 0.005; // Smaller for smoother animation

		// Points array for trail
		const points: { x: number; y: number; z: number; color: string }[] = [];
		let hue = 180; // Start at teal

		const loop = () => {
			width = canvas.parentElement?.clientWidth || 300;
			height = canvas.parentElement?.clientHeight || 300;

			if (canvas.width !== width || canvas.height !== height) {
				canvas.width = width;
				canvas.height = height;
				// Re-clear on resize but keep points? No, simple clear
				ctx.fillStyle = '#0a0f1c'; // Match math-dark
				ctx.fillRect(0, 0, width, height);
			}

			// Calculate next point (run multiple iterations per frame for speed)
			for (let i = 0; i < 5; i++) {
				const dx = sigma * (y - x) * dt;
				const dy = (x * (rho - z) - y) * dt;
				const dz = (x * y - beta * z) * dt;

				x += dx;
				y += dy;
				z += dz;

				points.push({ x, y, z, color: `hsl(${hue}, 100%, 50%)` });
				hue = (hue + 0.3) % 360;
			}

			if (points.length > 3000) {
				points.splice(0, 5);
			}

			// Render
			// Fade effect
			ctx.fillStyle = 'rgba(10, 15, 28, 0.03)';
			ctx.fillRect(0, 0, width, height);

			ctx.lineWidth = 1.5;

			// Scaling and centering
			const scale = 6;
			const cx = width / 2;
			const cy = height / 2;

			// Draw the last few segments for a continuous look
			ctx.beginPath();
			if (points.length > 2) {
				for (let i = Math.max(0, points.length - 6); i < points.length - 1; i++) {
					const p1 = points[i];
					const p2 = points[i + 1];

					// Project: use x for horizontal, z for vertical (top-down view of attractor)
					ctx.strokeStyle = '#2dd4bf';
					ctx.moveTo(cx + p1.x * scale, cy + (p1.z - 25) * scale); // Center Z around 25
					ctx.lineTo(cx + p2.x * scale, cy + (p2.z - 25) * scale);
				}
				ctx.stroke();
			}

			requestAnimationFrame(loop);
		};

		const animation = requestAnimationFrame(loop);
		return () => cancelAnimationFrame(animation);
	});
</script>

<div
	class="relative flex h-[400px] w-full items-center justify-center overflow-hidden rounded-2xl border border-white/5 bg-math-dark"
>
	<canvas bind:this={canvas} class="absolute inset-0 z-10"></canvas>
	<div class="absolute bottom-4 left-6 z-20 font-mono text-xs text-slate-500">
		Lorenz Attractor<br />
		dy/dt = x(ρ - z) - y
	</div>
</div>
