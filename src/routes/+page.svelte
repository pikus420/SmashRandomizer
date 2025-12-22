<script>
    import RandomButton from './RandomButton.svelte';
    import Display from './Display.svelte';
    import { roster, blacklist0, blacklist1, blacklist2, blacklist3 } from '$lib/roster.js';

    let curr_characters = $state(["None", "None", "None", "None"]);
    
    const all_blacklists = [blacklist0, blacklist1, blacklist2, blacklist3];
    const roster_length = roster.length;

    function randomizeChracter() {
        curr_characters = curr_characters.map((_, i) => {
            let character;
            let isBlacklisted = true;

            while (isBlacklisted) {
                const randomIndex = Math.floor(Math.random() * roster_length);
                character = roster[randomIndex];

                isBlacklisted = all_blacklists[i].includes(character);
            }

            return character;
        });
    }
</script>

<div class="flex flex-col items-center gap-8 p-10">
    <RandomButton klik={randomizeChracter} />

    <div class="flex flex-row flex-wrap justify-center gap-4 w-full">
        <Display character={curr_characters[0]} player="_pikus"/>
        <Display character={curr_characters[1]} player="Bomsii"/>
        <Display character={curr_characters[2]} player="Messi"/>
        <Display character={curr_characters[3]} player="Kuriboh"/>
    </div>
</div>