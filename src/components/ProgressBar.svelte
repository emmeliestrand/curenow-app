<script>
  export let barWidth = 10;
</script>

<div class="bar progress-bar-bg">
  <div class="bar progress-bar" style="width: {barWidth}%"></div>
</div>

<style>
  .bar {
    border-radius: var(--grid-base);
    height: var(--grid-base);
  }
  .progress-bar-bg {
    background-color: var(--white-100);
    margin: 0 3rem var(--grid-base) 3rem;
  }
  .progress-bar {
    background-color: var(--green-200);
    transition: width 2500ms;
  }

</style>