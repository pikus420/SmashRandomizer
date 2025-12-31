<script>
    import RandomButton from './RandomButton.svelte';
    import SingleRandomButton from './SingleRandomButton.svelte';
    import Display from './Display.svelte';
    import Portrait from './Portrait.svelte';
    import { roster, blacklist0, blacklist1, blacklist2, blacklist3 } from '$lib/roster.js';

    let curr_characters = $state(["None", "None", "None", "None"]);
        
        const players = [
            { name: "_pikus", blacklist: blacklist0 },
            { name: "Bomsii", blacklist: blacklist1 },
            { name: "Messi",  blacklist: blacklist2 },
            { name: "Kuriboh", blacklist: blacklist3 }
        ];

        const roster_length = roster.length;

        function reroll(i) {
            let character;
            do {
                character = roster[Math.floor(Math.random() * roster_length)];
            } while (players[i].blacklist.includes(character));
            
            curr_characters[i] = character;
        }

        function randomizeAll() {
            for (let i = 0; i < players.length; i++) {
                reroll(i);
            }
        }
    </script>

    <div class="flex flex-col items-center gap-8 p-10">
        <RandomButton click={randomizeAll} />

        <div class="flex flex-row flex-wrap justify-center gap-4 w-full">
            {#each players as p, i}
                <div class="flex flex-col items-center gap-2">
                    <Display character={curr_characters[i]} player={p.name}/>
                    <SingleRandomButton click={() => reroll(i)}/>
                    {#if curr_characters[i] != "None"}
                    <Portrait character={curr_characters[i]}/>
                    {/if}
                </div>
            {/each}
        </div>
    </div>