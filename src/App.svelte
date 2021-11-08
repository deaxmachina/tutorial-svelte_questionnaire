<script>
  import Header from "./components/Header.svelte"
  import Footer from "./components/Footer.svelte"
  import Tabs from "./shared/Tabs.svelte"
  import CreatePollForm from "./components/CreatePollForm.svelte"
  import PollList from "./components/PollList.svelte"

  // tabs //
  let items = ['Current Polls', 'Add New Poll']
  let activeItem = 'Current Polls'

  const tabChange = e => activeItem = e.detail

  // polls //
  let polls = [
    {
      id: 1, 
      question: 'Python or JavaScript',
      answerA: 'Python',
      answerB: 'JavaScript',
      votesA: 9,
      votesB: 15
    }
  ]
  const handleAdd = e => {
    polls = [e.detail, ...polls]
    console.log(polls)
    activeItem = 'Current Polls'
  }

  const handleVote = e => {
    // get data that was passed from child component
    const { id, option } = e.detail
    // make copy of the data to update it
    let copiedPolls = [...polls] 
    // find relevant poll to update
    let upvotedPoll = copiedPolls.find(poll => poll.id === id)
    // change the data on that poll 
    if (option === 'a') {
      upvotedPoll.votesA++
    } else if (option === 'b') {
      upvotedPoll.votesB++
    }
    // update the original votes array to reassign
    polls = copiedPolls
  }

</script>

<Header />
<main>
  <Tabs 
    items={items} activeItem={activeItem}
    on:tabChange={tabChange}
  />
  {#if activeItem === 'Current Polls'}
    <PollList polls={polls} on:vote={handleVote} />
  {:else if activeItem === 'Add New Poll'}
    <CreatePollForm on:add={handleAdd} />
  {/if}
</main>
<Footer />

<style>
  main {
    max-width: 960px;
    margin: 40px auto;
  }
</style>