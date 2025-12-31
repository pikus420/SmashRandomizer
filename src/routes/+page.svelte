<script>
    import RandomButton from './RandomButton.svelte';
    import SingleRandomButton from './SingleRandomButton.svelte';
    import Display from './Display.svelte';
    import Portrait from './Portrait.svelte';
    import { roster, blacklist0, blacklist1, blacklist2, blacklist3 } from '$lib/roster.js';

    let active_players = $state([
        { name: "_pikus", blacklist: blacklist0, character: "None", isGuest: false },
        { name: "Bomsii", blacklist: blacklist1, character: "None", isGuest: false },
        { name: "Messi",  blacklist: blacklist2, character: "None", isGuest: false },
        { name: "Kuriboh", blacklist: blacklist3, character: "None", isGuest: false }
    ]);

    const roster_length = roster.length;

    function reroll(index) {
        let new_char;
        const player = active_players[index];
        
        do {
            new_char = roster[Math.floor(Math.random() * roster_length)];
        } while (player.blacklist.includes(new_char)); 
        
        active_players[index].character = new_char;
    }

    function randomizeAll() {
        for (let i = 0; i < active_players.length; i++) {
            reroll(i);
        }
    }

    function addGuest() {
        active_players.push({
            name: "Guest", 
            blacklist: [],
            character: "None",
            isGuest: true
        });
    }

    function removePlayer(index) {
        active_players.splice(index, 1);
    }
</script>

<div class="flex flex-col items-center gap-8 p-10">
    <div class="flex gap-4">
        <RandomButton click={randomizeAll} />
        
        <button 
            class="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600 transition"
            onclick={addGuest}
        >
            + Add Guest
        </button>
    </div>

    <div class="flex flex-row flex-wrap justify-center gap-4 w-full">
        {#each active_players as p, i}
            <div class="relative flex flex-col items-center gap-2 p-4 border border-gray-200 rounded-lg">
                
                {#if p.isGuest}
                    <button 
                        class="absolute top-2 right-2 text-red-500 hover:text-red-700 font-bold"
                        onclick={() => removePlayer(i)}
                        aria-label="Remove guest"
                    >
                        ✕
                    </button>
                {/if}

                <Display character={p.character} player={p.name}/>
                
                <SingleRandomButton click={() => reroll(i)}/>
                
                {#if p.character !== "None"}
                    <Portrait character={p.character}/>
                {/if}
            </div>
        {/each}
    </div>
</div>