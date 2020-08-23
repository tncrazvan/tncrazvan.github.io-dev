<script>
import { onMount } from 'svelte';
import slotify from '../../../svelte-shared/scripts/slotify';
let content,footer,card;
onMount(()=>slotify(card,{"footer":footer,"content":content}));
</script>
<div bind:this={card} class="basic-card">
  <div bind:this={content} class="basic-card-content"></div>
  <div bind:this={footer} class="basic-card-footer"></div>
  <slot></slot>
</div>

<style>
  .basic-card{
    margin: 1rem;
    border-radius: 0.3rem;
    background: rgba(0,0,0,0.3);
    border: 1px solid rgba(0,0,0,0.3);
    box-shadow: 0 0 0.1rem 0.05rem rgba(0,0,0,0.1);
    transition: transform 200ms, border-color 200ms;
    -webkit-transition: transform 200ms, border-color 200ms;
    -moz-transition: transform 200ms, border-color 200ms;
    -o-transition: transform 200ms, border-color 200ms;
  }
  .basic-card-content,
  .basic-card-footer{
    padding: 1rem;
  }
  .basic-card-footer{
    background: #922a1a;
    border-top: 3px solid rgba(0,0,0,0.3);
    border-bottom-left-radius: 0.3rem;
    border-bottom-right-radius: 0.3rem;
  }
</style>