<script>
  import { onMount } from "svelte";
  import { scale } from "svelte/transition";

  export let onDone = () => {};

  let count = 22;
  onMount(() => {
    const timer = setInterval(() => {
      count -= 1;
      if (count <= 0) {
        clearInterval(timer);
        setTimeout(() => onDone(), 500);
      }
    }, 1000);
    return () => clearInterval(timer);
  });
</script>

<div class="loader-container">
  <div class="spinner-wrapper">
    <div class="spinner">
      <div class="spinner1"></div>
    </div>
    
    <div class="number-wrapper">
      {#key count}
        <span in:scale={{ start: 0.5 }} class="count-number">
          {count > 0 ? count : "Listooo"}
        </span>
      {/key}
    </div>
  </div>
  
  <h2 class="loading-text">
    Cargando Sorpresa...
  </h2>
</div>

<style>
  /* 1. Estilos del Contenedor Principal (Reemplaza a Tailwind flex/h-full/bg) */
  .loader-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh; /* Ocupa toda la altura de la pantalla */
    width: 100%;
    color: white;
    position: relative;
    overflow: hidden;
  }

  .spinner-wrapper {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  /* 2. Estilos del Spinner */
  .spinner {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    position: relative;
    border: 4px solid rgba(255, 255, 255, 0.1);
  }

  .spinner1 {
    position: absolute;
    top: -4px;
    left: -4px;
    width: 100%;
    height: 100%;
    border-radius: 50%;
    border: 4px solid transparent;
    /* Borde superior e inferior con color brillante */
    border-top-color: #00d2ff; 
    border-right-color: #3a7bd5; 
    /* Agregamos box-content para que el borde no reduzca el tamaño */
    box-sizing: content-box;
    animation: spin 1s linear infinite;
  }

  /* 3. Estilos del Número */
  .number-wrapper {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .count-number {
    font-size: 2.5rem; /* Equivalente a text-4xl */
    font-weight: bold;
    color: white;
    text-shadow: 0 2px 4px rgba(0,0,0,0.3);
    font-family: sans-serif;
  }

  /* 4. Estilos del Texto inferior */
  .loading-text {
    margin-top: 2rem;
    font-weight: 300;
    letter-spacing: 0.1em;
    opacity: 0.9;
    font-family: sans-serif;
    animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
  }

  /* Animaciones */
  @keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }

  @keyframes pulse {
    0%, 100% { opacity: 1; }
    50% { opacity: .5; }
  }
</style>