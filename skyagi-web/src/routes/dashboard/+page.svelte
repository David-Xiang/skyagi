<script lang="ts">
    import Character from '$lib/dashboard-character.svelte';
    import { AccordionItem, Accordion, Button} from 'flowbite-svelte';
    import Conversation from '$lib/dashboard-conversation.svelte'
    export let data;
    export const characterData = data.agents.agents
    export const conversationData = data.conversations.conversations
    console.log(conversationData)
    

    const characters = characterData.map((characterDataPoint) => ({
        ...characterDataPoint,
        image: "../src/lib/assets/Avatar1.png"
    }))
    export const conversations = conversationData.map((conversationDataPoint) => ({
        ...conversationDataPoint
    }))

</script>


<div id="globalGrid">
    <div>
        <Accordion id="conversationBoard">
            {#each conversations as conversation, i}
                <Conversation conversationIndex={i+1} conversationSummary = {conversation.conversationSummary} >
                </Conversation>
            {/each}
        </Accordion>
        <div id="buttonGrid">
            <Button>
                Create new conversation
            </Button>
            <Button>
                Create new agent
            </Button>
        </div>
    </div>
    
    <div class="scroller">
        {#each characters as character, i}
            <div class="characterInfoSet">
                <Character {character}>
                </Character>
            </div>
        {/each}
    </div>

</div>




<style>

    #conversationBoard {
        height: 1000px;
    }


    .scroller {
        width: 600px;
        height: 500px;
        top: 20px;
        position: relative;
        overflow-x: scroll;
        overflow-y: scroll;
        display: grid;
        grid-template-columns: repeat(3, 200px);
        grid-template-rows: repeat(auto-fill, 220px);
    }

    #globalGrid {
        display: grid;
        grid-template-columns: repeat(2, 40%);
        grid-auto-flow: column;
        gap: 10px;
        /* grid-auto-columns: 400px 400px; */
    }

    #buttonGrid {
        display: grid;
        grid-template-rows: (2, 50%);
    }

</style>