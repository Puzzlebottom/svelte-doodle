<script>
  export let id;
  let dragging = false;
  let top = 0;
  let left = 0;

  const grab = () => {
    dragging = true;
  };

  const release = () => {
    dragging = false;
  };

  const drag = (e) => {
    if (dragging) {
      left = left + e.movementX;
      top = top + e.movementY;
    }
  };

  const agents = [];
</script>

<svelte:window on:mouseup={release} on:mousemove={(e) => drag(e)} />

<div class="container">
  <div
    class="cluster"
    on:mousedown={grab}
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
