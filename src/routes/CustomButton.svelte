<script lang="ts">
  type labelType = '+' | '-' | '0' | '×';

  export let label: labelType;
  export let onClick: () => void = () => {};
  export let className = '';

  const textColor = label === "×" ? "text-black" : "text-white";
</script>

<button class={`w-8 h-8 ${textColor} ${className}`} tabindex="-1" on:click={onClick}>
  {label}
</button> 