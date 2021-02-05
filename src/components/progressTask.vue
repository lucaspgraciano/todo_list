<template>
  <div class="tasks-progress">
      <span class="progress-value">{{ progress }}%</span>
      <div class="progress-bar" :style="{width: progress + '%' }"></div>
  </div>
</template>

<script>
export default {
    props: {
        progress: { type: Number, default: 0}
    }
}
</script>

<style>
    .tasks-progress{
        animation: progressBar 1s;
        position: relative;
        width: 502px;
        background-color: #fff;
        margin: 5px auto 10px auto;
        color: #111;
        display: flex;
        align-items: center;
        flex-direction: column;
    }
    .progress-bar{
        position: absolute;
        height: 100%;
        background-color: greenyellow;
        align-self: flex-start;
    }
    .progress-value{
        z-index: 1;
    }
    @keyframes progressBar {
        0%{ width: 50px;}
        100%{width: 502px;}
    }

</style>