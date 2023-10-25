<script>
  export let id;
  export let top;
  export let left;
  export let border;
  export let grab;
</script>

<div class="container">
  <div
    class="agent"
    on:mousedown={() => grab("agent", id)}
    style:left={`${left}px`}
    style:top={`${top}px`}
    style:border-color={border}
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
    border-radius: 50%;
    background-color: rgb(60, 60, 60);
    color: white;
    height: 100px;
    width: 100px;
  }
</style>
