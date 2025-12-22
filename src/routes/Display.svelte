<script>
    let { player, character } = $props();
</script>

<div class="w-48 p-4 bg-white border border-slate-200 rounded-lg shadow-sm flex flex-col gap-2 shrink-0">
    <div class="flex flex-col">
        <span class="text-[9px] font-black uppercase text-slate-400">Player</span>
        <span class="font-bold text-slate-800 truncate">{player}</span>
        <img src="/img/{player}.png" alt="{player}'s avatar" class="rounded-full size-20">
    </div>
    
    <div class="border-t border-slate-100 my-1"></div>

    <div class="flex flex-col">
        <span class="text-[9px] font-black uppercase text-blue-500">Character</span>
        <span class="font-medium text-blue-700 truncate">{character}</span>
    </div>
</div>