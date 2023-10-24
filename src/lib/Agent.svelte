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
</script>

<svelte:window on:mouseup={release} on:mousemove={(e) => drag(e)} />

<div class="container">
  <div
    class="agent"
    on:mousedown={grab}
    style:left={`${left}px`}
    style:top={`${top}px`}
    tabindex={id}
    role="button"
  >
    Agent {id}
  </div>
</div>

<style>
  div.container {
    height: 0;
    width: 0;
  }
  div.agent {
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    border: thick solid;
    border-color: gray;
    border-radius: 50%;
    background-color: rgb(60, 60, 60);
    color: white;
    height: 100px;
    width: 100px;
  }
</style>
