<script lang="ts">
    import { default as Particles, particlesInit } from '@tsparticles/svelte';
    import { onMount } from 'svelte';
    import { loadFull } from 'tsparticles';

    let ParticlesComponent: typeof Particles;

	const particlesConfig = {
		particles: {
			color: {
				value: '#000'
			},
			links: {
				enable: true,
				color: '#000'
			},
			move: {
				enable: true
			},
			number: {
				value: 100
			}
		}
	};

    const onParticlesLoaded = (event: CustomEvent<any>) => {
		const particlesContainer = event.detail.particles;

		// you can use particlesContainer to call all the Container class
		// (from the core library) methods like play, pause, refresh, start, stop

        particlesContainer.play();
	};

    void particlesInit(async (engine) => {
        await loadFull(engine);
    });

    onMount(async () => {
        ParticlesComponent = await import('@tsparticles/svelte').then((o) => o.default);
    });
</script>

{#if ParticlesComponent}
    <svelte:component this={ParticlesComponent} options={particlesConfig} on:onParticlesLoaded={onParticlesLoaded} />
{/if}
