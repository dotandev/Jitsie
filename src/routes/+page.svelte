<script lang="ts">
	import JitsiMeeting from "$lib/JitsiMeeting.svelte";

	let roomInput = "";
	let isOpen = false;

	function openMeeting() {
		if (roomInput.trim()) {
			isOpen = true;
		}
	}

	function closeMeeting() {
		isOpen = false;
	}
</script>

<style>
	.modal-bg {
		background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
		animation: pulse-bg 5s infinite ease-in-out;
	}

	@keyframes pulse-bg {
		0%, 100% { filter: hue-rotate(0deg); }
		50% { filter: hue-rotate(90deg); }
	}

	.modal-content {
		background: white;
		border: 5px solid cyan;
		border-radius: 24px;
		padding: 2rem;
		box-shadow: 0 0 50px cyan;
		animation: bounceIn 0.6s ease;
		max-height: 90vh;
		overflow: hidden;
	}

	@keyframes bounceIn {
		0% {
			opacity: 0;
			transform: scale(0.8) translateY(50px);
		}
		100% {
			opacity: 1;
			transform: scale(1) translateY(0);
		}
	}
</style>

<div class="p-8 text-center flex justify-center">
	<h1 style="font-size: 3rem; color: blue; font-weight: bold">
		Welcome to Kenzy Meet!
	</h1>
	<p style="font-size: 1.5rem; margin: 1rem 0; color: magenta">
		Type a meeting room name and launch!
	</p>
	<input
		bind:value={roomInput}
		placeholder="Enter room name..."
		style="padding: 1rem; font-size: 1.2rem; border: 3px solid pink; border-radius: 12px; width: 300px;"
	/>
	<br />
	<button
		on:click={openMeeting}
		style="margin-top: 1rem; padding: 1rem 2rem; font-size: 1.2rem; background: limegreen; color: white; border: none; border-radius: 12px; box-shadow: 0 0 10px green; cursor: pointer;"
	>
		🚀 Join Now
	</button>
</div>

{#if isOpen}
	<div
		class="fixed inset-0 z-50 flex items-center justify-center modal-bg"
	>
		<div class="modal-content relative w-[90%] max-w-5xl">
			<button
				on:click={closeMeeting}
				style="position: absolute; top: 1rem; right: 1rem; font-size: 2rem; color: red; background: transparent; border: none; cursor: pointer;"
			>
				✖
			</button>
			<JitsiMeeting roomName={roomInput} />
		</div>
	</div>
{/if}
