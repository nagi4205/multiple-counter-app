<script lang="ts">
  type labelType = '+' | '-' | '0' | '×';

  export let label: labelType;
  export let onClick: () => void = () => {};
  export let className = '';
</script>

<button class={`w-8 h-8 ${className}`} tabindex="-1" on:click={onClick}>
  {label}
</button> 