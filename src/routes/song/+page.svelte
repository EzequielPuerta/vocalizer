<script lang="ts">
    import { page } from "$app/stores";

    let lyric = "";

    function extractVowels(text: string): string {
        const vowels = ["a", "e", "i", "o", "u"];
        const accentedVowelsMap: Record<string, string> = {
            á: "a", é: "e", í: "i", ó: "o", ú: "u", ü: "u",
        };

        return text
            .split(/\s+/)
            .map(word => {
                let result = "";
                for (let i = 0; i < word.length; i++) {
                    const char = word[i].toLowerCase();

                    if (char === "y") {
                        if (i === word.length - 1 || /[aeiouáéíóú]/i.test(word[i + 1]) === false) {
                            result += "I";
                        }
                        continue;
                    }

                    if (char === "u" && i > 0 && word[i - 1].toLowerCase() === "q") {
                        continue;
                    }

                    if (vowels.includes(char)) {
                        result += char.toUpperCase();
                    } else if (accentedVowelsMap[char]) {
                        result += accentedVowelsMap[char].toUpperCase();
                    }
                }
                return result;
            })
            .join("   ");
    }

    $: lyric = $page.url.searchParams.get("lyric") || "";

    $: lyricFormatted = lyric
        .split("\n")
        .map(line => line.trim())
        .filter(line => !/^\[.*\]$/.test(line))
        .map(line => {
            const vocalLine = extractVowels(line);
            return `<span class="text-secondary">${vocalLine}</span>\n${line}`;
        })
        .join("\n\n");
</script>

<div class="p-16 max-w-3xl mx-auto">
    <h1 class="text-3xl font-bold mb-4">Letra Vocalizada:</h1>
    <div class="divider"></div>
    <div class="bg-gray-900 text-white p-6 rounded-lg whitespace-pre-wrap">
        {@html lyricFormatted.replace(/\n/g, "<br>")}
    </div>
</div>
