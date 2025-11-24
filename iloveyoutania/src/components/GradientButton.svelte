<script>
  // Recibimos la clase extra si es necesaria
  export let className = "";
  // En Svelte, los eventos de clic se propagan automáticamente si usamos on:click sin argumentos,
  // pero si queremos pasar una prop explícita como en React:
  export let onClick = () => {};
</script>

<button
  on:click={onClick}
  class="px-10 py-4 rounded-full text-white font-semibold text-lg
         bg-gradient-to-r from-pink-500 via-rose-500 to-fuchsia-500
         shadow-[0_0_28px_rgba(244,114,182,0.35)]
         transition-transform duration-200 ease-out hover:scale-[1.03] active:scale-95
         focus:outline-none focus-visible:ring-2 focus-visible:ring-pink-300/70 
         flex gap-2 items-center justify-center {className}"
>
  <!-- El slot renderiza lo que pongas dentro del componente <GradientButton> -->
  <slot />
</button>