<script lang="ts">
	import '../app.css';
	import favicon from '$lib/assets/favicon.png';
    import { injectAnalytics } from '@vercel/analytics/sveltekit'

    injectAnalytics();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<div class="flex flex-col min-h-screen">
    <div class="navbar bg-neutral fixed top-0 left-0 right-0 w-full z-50 flex items-center">
        <a href="/" class="btn btn-ghost text-xl text-white">
            Vocalizer
        </a>
    </div>

    <slot />

    <footer class="footer sm:footer-horizontal footer-center bg-primary text-base-content p-5 z-100">
        <aside>
            <p>Copyleft 🄯 {new Date().getFullYear()} - Todos los derechos sin reservar</p>
        </aside>
    </footer>
</div>