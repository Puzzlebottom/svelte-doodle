<script>
  import Agent from "./lib/Agent.svelte";
  import Cluster from "./lib/Cluster.svelte";

  const addCluster = () => {
    const newCluster = { id: clusters.length, top: 0, left: 0 };
    clusters = [...clusters, newCluster];
  };

  const addAgent = () => {
    const newAgent = { id: agents.length, top: 0, left: 0, border: "gray" };
    agents = [...agents, newAgent];
  };

  const grab = (entity, id) => {
    dragging = { entity, id };
  };

  const drag = (e) => {
    if (dragging && dragging.entity === "agent") {
      const agent = agents.find((agent) => agent.id === dragging.id);
      const top = agent.top + e.movementY;
      const left = agent.left + e.movementX;
      const updatedAgent = { ...agent, top, left };
      console.log(agents.filter((agent) => agent.id !== dragging.id));

      agents = [
        ...agents.filter((agent) => agent.id !== dragging.id),
        updatedAgent,
      ];
    }
    if (dragging && dragging.entity === "cluster") {
      const cluster = clusters.find((cluster) => cluster.id === cluster.id);
      const top = cluster.top + e.movementY;
      const left = cluster.left + e.movementX;
      const updatedCluster = { ...cluster, top, left };

      clusters = [
        ...clusters.filter((cluster) => cluster.id !== dragging.id),
        updatedCluster,
      ];
    }
  };

  const release = () => {
    dragging = null;
  };

  let dragging = null;

  let clusters = [];
  let agents = [];
</script>

<svelte:window on:mouseup={release} on:mousemove={(e) => drag(e)} />

<main>
  <div class="button-container">
    <button on:click={addCluster}>NEW CLUSTER</button>
    <button on:click={addAgent}>NEW AGENT</button>
  </div>
  <div class="container">
    {#each clusters as cluster}
      <Cluster id={cluster.id} top={cluster.top} left={cluster.left} {grab} />
    {/each}
    {#each agents as agent}
      <Agent
        id={agent.id}
        border={agent.border}
        top={agent.top}
        left={agent.left}
        {grab}
      />
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
