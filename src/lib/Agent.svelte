<script>
  export let id;
  let dragging = false;
  let top = 0;
  let left = 0;

  const grab = (e) => {
    dragging = true;
  };

  const release = (e) => {
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
    on:mousedown={(e) => grab(e)}
    style:left={`${left}px`}
    style:top={`${top}px`}
    tabindex={id}
    role="button"
  >
    {id}
  </div>
</div>

<style>
  div.container {
    height: 1;
    width: 1;
  }
  div.agent {
    position: relative;
    display: flex;
    justify-self: center;
    align-self: center;
    justify-content: center;
    align-items: center;
    border: thick solid;
    border-color: gray;
    border-radius: 50%;
    color: white;
    height: 100px;
    width: 100px;
  }
</style>
