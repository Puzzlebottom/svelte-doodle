<script>
  import Agent from "./lib/Agent.svelte";
  import Cluster from "./lib/Cluster.svelte";

  const addCluster = () => {
    clusters = [...clusters, { id: clusters.length }];
  };

  const addAgent = () => {
    agents = [...agents, { id: agents.length }];
  };

  const clusterAgent = (agent, cluster) => {};

  let clusters = [];
  let agents = [];
</script>

<main>
  <div class="button-container">
    <button on:click={addCluster}>NEW CLUSTER</button>
    <button on:click={addAgent}>NEW AGENT</button>
  </div>
  <div class="container">
    {#each clusters as cluster}
      <Cluster id={cluster.id} />
    {/each}
    {#each agents as agent}
      <Agent id={agent.id} />
    {/each}
  </div>
</main>

<style>
  div.button-container {
    display: flex;
    flex-direction: column;
    width: fit-content;
  }
</style>
