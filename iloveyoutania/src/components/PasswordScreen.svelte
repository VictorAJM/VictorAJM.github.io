<script>
  import { fade, fly } from "svelte/transition";
  import GradientButton from "./GradientButton.svelte";
  import { Lock, ArrowRight, KeyRound } from "lucide-svelte";

  export let onNext = () => {};

  let password = "";
  let error = false;
  let shake = false;

  // 🔒 CONFIGURACIÓN: Cambia esto por la contraseña que quieras
  const CORRECT_PASSWORD = "SeleneMireles0."; 

  function handleSubmit() {
    // Convertimos a minúsculas para que no importen las mayúsculas
    console.log(password);
    if (password.trim() === CORRECT_PASSWORD) {
      error = false;
      onNext();
    } else {
      triggerError();
    }
  }

  function triggerError() {
    error = true;
    shake = true;
    setTimeout(() => {
      shake = false; // Detener la animación después de 500ms
    }, 500);
  }
</script>

<div class="py-10 md:py-14 text-center min-h-[600px] flex flex-col justify-center items-center">
  
  <div class="flex flex-col items-center gap-6 w-full max-w-md px-4">
    
    <!-- Ícono o Imagen de Candado -->
    <div 
      in:fly={{ y: -20, duration: 800 }}
      class="mb-4 relative"
    >
      <div class="absolute inset-0 bg-pink-500/20 blur-xl rounded-full animate-pulse"></div>
      <div class="relative bg-gradient-to-br from-pink-100 to-white p-6 rounded-full shadow-[0_0_30px_rgba(236,72,153,0.3)] border border-white/50">
        <Lock class="w-12 h-12 text-pink-500" />
      </div>
    </div>

    <!-- Títulos -->
    <div in:fly={{ y: 20, duration: 800, delay: 200 }}>
      <h1 
        class="text-pretty text-3xl md:text-5xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-violet-400 via-fuchsia-400 to-pink-400 drop-shadow leading-tight mb-4"
        style="filter: drop-shadow(0 0 20px rgba(255,105,180,0.4));"
      >
        Hola Tania Linda Preciosa :)
      </h1>
      <p class="text-xl text-pink-200">
        Para acceder a la sorpresa, ingresa tu contraseña :P
      </p>
    </div>

    <!-- Input de Contraseña -->
    <form 
      on:submit|preventDefault={handleSubmit}
      in:fly={{ y: 20, duration: 800, delay: 400 }}
      class="w-full flex flex-col items-center gap-4 mt-4"
    >
      <div class="relative w-full max-w-xs {shake ? 'animate-shake' : ''}">
        <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
          <KeyRound class="h-5 w-5 text-pink-300/70" />
        </div>
        
        <input
          type="text"
          bind:value={password}
          placeholder="Escribe aquí..."
          class="block w-full pl-10 pr-4 py-4 rounded-full 
                 bg-white/10 border border-white/20 
                 text-white placeholder-pink-200/50 text-center text-lg
                 focus:outline-none focus:ring-2 focus:ring-pink-400 focus:border-transparent
                 transition-all duration-300 backdrop-blur-sm
                 {error ? 'border-red-400 ring-red-400/50 bg-red-900/10' : ''}"
        />
      </div>

      {#if error}
        <p in:fade class="text-rose-300 font-medium text-sm">
          JAJAJAJ, esa no es
        </p>
      {/if}

      <div class="mt-8">
        <GradientButton 
          onClick={handleSubmit} 
          className="bg-white text-black px-8 py-3 rounded-full font-bold shadow-lg hover:shadow-pink-500/20 transition-all"
        >
          DESBLOQUEAR
          <ArrowRight size={20} class="mt-0.5 ml-2" />
        </GradientButton>
      </div>
    </form>

  </div>
</div>

<style>
  /* Animación de temblor para cuando la contraseña está mal */
  .animate-shake {
    animation: shake 0.5s cubic-bezier(.36,.07,.19,.97) both;
  }

  @keyframes shake {
    10%, 90% { transform: translate3d(-1px, 0, 0); }
    20%, 80% { transform: translate3d(2px, 0, 0); }
    30%, 50%, 70% { transform: translate3d(-4px, 0, 0); }
    40%, 60% { transform: translate3d(4px, 0, 0); }
  }
</style>