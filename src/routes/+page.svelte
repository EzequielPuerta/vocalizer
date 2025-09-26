<script lang="ts">
    import { goto } from "$app/navigation";

    let lyric = "";

    function vocalize() {
        goto(`/song?lyric=${encodeURIComponent(lyric)}`);
    }
</script>

<div
    class="hero min-h-screen"
    style="background-image: url(https://i0.wp.com/thevocalcoachlondon.com/wp-content/uploads/2024/12/best-microphone-for-vocalists-professional-recording.jpg?fit=1280%2C854&ssl=1);"
>
    <div class="hero-overlay bg-gradient-to-b from-black/90 to-black/30"></div>
    <div class="hero-content text-neutral-content text-center">
        <div class="max-w-md bg-black/75 rounded-xl p-10">
            <h1 class="mb-5 text-5xl font-bold text-primary">Vocalizer</h1>
            <h2 class="mb-5 text-xl">
                Para cuando la <em class="text-secondary">Rusa</em> te mande a cantar con las vocales! 😉
            </h2>
            <textarea
                bind:value={lyric}
                placeholder="Pega aquí la letra de la canción..."
                class="textarea textarea-bordered w-full mb-4"
                rows="6"
            ></textarea>
            <button class="btn btn-primary w-full" on:click={vocalize}>
                Vocalizar!
            </button>
        </div>
    </div>
</div>