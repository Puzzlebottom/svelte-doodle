<script>
  import Agent from "./lib/Agent.svelte";
  import Cluster from "./lib/Cluster.svelte";

  const addCluster = () => {
    clusters = [...clusters, "cluster"];
  };

  const addAgent = () => {
    agents = [...agents, "agent"];
  };

  const clusterAgent = (agent, cluster) => {};

  let clusters = [];
  let agents = [];
</script>

<main>
  <button on:click={addCluster}>NEW CLUSTER</button>
  <button on:click={addAgent}>NEW AGENT</button>
  {#each clusters as cluster}
    <Cluster />
  {/each}
  {#each agents as agent}
    <Agent />
  {/each}
</main>

<style>
</style>
