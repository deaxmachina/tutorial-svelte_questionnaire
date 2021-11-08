<script>
  import { fade, slide, scale } from 'svelte/transition'
  import { flip } from 'svelte/animate'
  import { onMount, onDestroy } from 'svelte'
  import PollStore from "../stores/PollStore.js"
  import PollDetail from "./PollDetail.svelte"

  // export let polls = []

  // const unsub = PollStore.subscribe(data => {
  //   polls = data
  // })

  // onMount(() => {
  //   console.log('component mounted')
  // })

  // onDestroy(() => {
  //   console.log('component removed from the dom')
  //   // to unsubscribe from the data store
  //   unsub()
  // })

  // Alternative of the above - subscribe and unsubscibe at the same time $PollStore below instead of polls


</script>

<div class='poll-list'>
  {#each $PollStore as poll (poll.id)}
    <div in:fade out:scale|local animate:flip={{duration: 500}}>
      <PollDetail poll={poll} />
    </div>
  {/each}
</div>

<style>
  .poll-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
</style>