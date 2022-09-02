<style>
  img{
    max-height: 100vh;
    min-height: 00px;
    max-width: 90vw;
    min-width: 00px;
  }
  .preview_holder{
    position: fixed;
    top:10vh;
    left:0;
    z-index: 0;
    background-color: rgba(0, 0, 0, 0.275);
    width: 100vw;;
  }
</style>


<div class="preview_holder" in:fade >
      <img  src={img_src} alt=" "/>
      
</div>

<script>
    import {fade} from 'svelte/transition'
    export let img_src=""
</script>