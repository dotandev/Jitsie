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

<div class="p-4">
    <h2 class="text-xl font-bold mb-2">Enter Meeting Room</h2>
    <input
        bind:value={roomInput}
        placeholder="Enter room name..."
        class="border px-3 py-2 rounded w-full max-w-md"
    />
    <button
        on:click={openMeeting}
        class="mt-3 px-4 py-2 bg-blue-600 text-white rounded hover:bg-blue-700"
    >
        Join
    </button>
</div>

{#if isOpen}
    <div
        class="fixed inset-0 bg-black/70 z-50 flex items-center justify-center"
    >
        <div
            class="bg-white w-[90%] max-w-5xl p-4 rounded-xl shadow-lg relative"
        >
            <button
                on:click={closeMeeting}
                class="absolute top-2 right-2 text-gray-500 hover:text-red-500"
            >
                ✖
            </button>
            <JitsiMeeting roomName={roomInput} />
        </div>
    </div>
{/if}
