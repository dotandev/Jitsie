
<script lang="ts">
	import { onMount, onDestroy } from "svelte";

	export let roomName: string;
	let container: HTMLDivElement;
	let api: any;

	async function loadJitsiScript(): Promise<void> {
		return new Promise((resolve, reject) => {
			if ((window as any).JitsiMeetExternalAPI) return resolve();

			const script = document.createElement("script");
			script.src = "https://meet.jit.si/external_api.js";
			script.async = true;
			script.onload = () => resolve();
			script.onerror = () => reject("Failed to load Jitsi API");
			document.body.appendChild(script);
		});
	}

	onMount(async () => {
		await loadJitsiScript();

		api = new (window as any).JitsiMeetExternalAPI("meet.jit.si", {
			roomName,
			parentNode: container,
			width: "100%",
			height: "100%",
		});
	});

	onDestroy(() => {
		if (api) api.dispose();
	});
</script>

<div bind:this={container} class="meeting-container"></div>

<style>
	.meeting-container {
		width: 100%;
		height: 80vh;
		border: 3px dashed hotpink;
		box-shadow: 0 0 30px magenta;
		animation: wiggle 3s infinite ease-in-out;
		border-radius: 20px;
	}
	@keyframes wiggle {
		0% { transform: rotate(0deg) scale(1); }
		25% { transform: rotate(1deg) scale(1.02); }
		50% { transform: rotate(0deg) scale(1); }
		75% { transform: rotate(-1deg) scale(1.02); }
		100% { transform: rotate(0deg) scale(1); }
	}
</style>
