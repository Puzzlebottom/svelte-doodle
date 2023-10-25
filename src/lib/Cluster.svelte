<script>
  export let id;
  export let top;
  export let left;
  export let grab;

  const agents = [];
</script>

<div class="container">
  <div
    class="cluster"
    on:mousedown={() => grab("cluster", id)}
    style:left={`${left}px`}
    style:top={`${top}px`}
    tabindex={id}
    role="button"
  >
    Cluster {id}
  </div>
</div>

<style>
  div.container {
    height: 0;
    width: 0;
  }
  div.cluster {
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    border: thick solid;
    border-radius: 50%;
    border-color: red;
    height: 200px;
    width: 200px;
  }
</style>
