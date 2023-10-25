<script>
  import Agent from "./lib/Agent.svelte";
  import Cluster from "./lib/Cluster.svelte";

  let dragging = null;
  let clusters = [];
  let agents = [];

  const addCluster = () => {
    const newCluster = {
      id: clusters.length,
      top: 0,
      left: 0,
      agents: [],
      grab,
    };
    clusters = [...clusters, newCluster];
  };

  const updateClusters = (cluster) => {
    clusters = [...clusters.filter((c) => c.id !== cluster.id), cluster];
  };

  const addAgent = () => {
    const newAgent = {
      id: agents.length,
      top: 0,
      left: 0,
      border: "gray",
      grab,
    };
    agents = [...agents, newAgent];
  };

  const updateAgents = (agent) => {
    agents = [...agents.filter((a) => a.id !== agent.id), agent];
  };

  const grab = (entity, id) => {
    dragging = { entity, id };
  };

  const drag = (e) => {
    if (dragging && dragging.entity === "agent") {
      const agent = agents.find((agent) => agent.id === dragging.id);
      const updatedAgent = {
        ...agent,
        top: agent.top + e.movementY,
        left: agent.left + e.movementX,
      };

      updatedAgent.border = clusters.some((cluster) =>
        isOverlapping(updatedAgent, cluster)
      )
        ? "red"
        : "gray";

      updateAgents(updatedAgent);
    }
    if (dragging && dragging.entity === "cluster") {
      const cluster = clusters.find((cluster) => cluster.id === dragging.id);
      const updatedCluster = {
        ...cluster,
        top: cluster.top + e.movementY,
        left: cluster.left + e.movementX,
      };
      updateClusters(updatedCluster);
    }
  };

  const release = () => {
    if (dragging && dragging.entity === "agent") {
      const agent = agents.find((agent) => agent.id === dragging.id);
      clusters.forEach((cluster) => {
        if (isOverlapping(agent, cluster)) {
          clusterAgent(agent, cluster);
        }
      });
    }
    dragging = null;
  };

  const clusterAgent = (agent, cluster) => {
    const updatedCluster = {
      ...cluster,
      agents: [...cluster.agents.filter((id) => id !== agent.id), agent.id],
    };
    updateClusters(updatedCluster);
  };

  const isOverlapping = (agent, cluster) => {
    const clusterCenter = { x: cluster.left + 100, y: cluster.top + 100 };
    const agentCenter = { x: agent.left + 50, y: agent.top + 50 };

    const distance = Math.sqrt(
      Math.pow(clusterCenter.x - agentCenter.x, 2) +
        Math.pow(clusterCenter.y - agentCenter.y, 2)
    );

    return distance < 100 + 50;
  };
</script>

<svelte:window on:mouseup={release} on:mousemove={(e) => drag(e)} />

<main>
  <div class="button-container">
    <button on:click={addCluster}>NEW CLUSTER</button>
    <button on:click={addAgent}>NEW AGENT</button>
  </div>
  <div class="container">
    {#each clusters as cluster}
      <Cluster {...cluster} />
    {/each}
    {#each agents as agent}
      <Agent {...agent} />
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
