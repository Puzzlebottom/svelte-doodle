<script>
  import Agent from "./lib/Agent.svelte";
  import Cluster from "./lib/Cluster.svelte";

  const addCluster = () => {
    clusters = [...clusters, clusters.length];
  };

  const addAgent = () => {
    agents = [...agents, agents.length];
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
  <div class="cluster-container">
    {#each clusters as cluster}
      <Cluster />
    {/each}
    {#each agents as agent}
      <Agent />
    {/each}
  </div>
</main>

<style>
  div.button-container {
    display: flex;
    flex-direction: column;
    width: fit-content;
  }

  div.cluster-container {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
  }
</style>
