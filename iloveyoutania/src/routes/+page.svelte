<script>
  import { scale, fade, fly } from "svelte/transition";
  import { cubicOut } from "svelte/easing";
  import "../app.css";

  // Importa tus componentes
  import LoaderScreen from "../components/LoaderScreen.svelte";
  import IntroScreen from "../components/IntroScreen.svelte";
  import CakeScreen from "../components/CakeScreen.svelte";

  let currentScreen = 0;
  let flowComplete = false;

  // Define el flujo de pantallas aquí
  const screens = [
    { component: LoaderScreen, props: { onDone: () => nextScreen() } },
    { component: IntroScreen, props: { onNext: () => nextScreen() } },
    { component: CakeScreen, props: { onNext: () => nextScreen() } },
  ];

  function nextScreen() {
    if (currentScreen < screens.length - 1) {
      currentScreen += 1;
    } else {
      flowComplete = true; // Cuando termina el CakeScreen, mostramos el mensaje final
    }
  }

  // Transición personalizada
  function fadeScale(node, { delay = 0, duration = 800, start = 0.95 }) {
    const o = +getComputedStyle(node).opacity;
    return {
      delay,
      duration,
      css: t => {
        const eased = cubicOut(t);
        return `
          opacity: ${t * o};
          transform: scale(${start + (1 - start) * eased});
        `;
      }
    };
  }
</script>

<main class="min-h-screen bg-slate-950 relative overflow-hidden font-sans selection:bg-fuchsia-500 selection:text-white">
  
  <div class="absolute top-[-10%] left-[-10%] w-[500px] h-[500px] bg-purple-600/20 rounded-full blur-[120px] animate-pulse-slow pointer-events-none"></div>
  <div class="absolute bottom-[-10%] right-[-10%] w-[600px] h-[600px] bg-rose-600/20 rounded-full blur-[120px] animate-pulse-slow pointer-events-none" style="animation-delay: 2s;"></div>
  <div class="absolute inset-0 bg-[url('https://grainy-gradients.vercel.app/noise.svg')] opacity-20 pointer-events-none"></div>

  <div class="relative z-10 grid min-h-screen w-full place-items-center p-4 md:p-6">
    
    {#if !flowComplete}
      {#key currentScreen}
        <div
          in:fadeScale={{ start: 0.95, duration: 1000 }} 
          out:fade={{ duration: 600 }}
          class="col-start-1 row-start-1 w-full flex justify-center max-w-2xl"
        >
          <div class="relative w-full">
            <div class="absolute inset-0 bg-gradient-to-r from-fuchsia-500/10 to-purple-500/10 blur-2xl -z-10 rounded-full opacity-50"></div>
            
            <svelte:component 
              this={screens[currentScreen].component} 
              {...screens[currentScreen].props} 
            />
          </div>
        </div>
      {/key}

    {:else}
      <div 
        in:fly={{ y: 20, duration: 1000, easing: cubicOut }} 
        class="col-start-1 row-start-1 text-center relative"
      >
        <div class="bg-white/5 backdrop-blur-xl border border-white/10 p-10 md:p-14 rounded-3xl shadow-[0_0_50px_rgba(0,0,0,0.5)] max-w-lg mx-auto">
          
          <div class="mb-6 inline-block p-4 rounded-full bg-gradient-to-br from-fuchsia-500/20 to-rose-500/20 border border-white/5 shadow-inner">
             <svg xmlns="http://www.w3.org/2000/svg" class="w-12 h-12 text-pink-300" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
               <path stroke-linecap="round" stroke-linejoin="round" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" />
             </svg>
          </div>

          <h1 class="text-4xl md:text-5xl font-black text-transparent bg-clip-text bg-gradient-to-r from-white via-pink-100 to-white drop-shadow-sm mb-4">
            Hola, Tania Linda Preciosa
          </h1>
          
          <p class="text-lg text-white/60 font-light leading-relaxed mb-8">
            Hice esto con mucho cariño, ¡te mereces lo mejor!
          </p>
        </div>
      </div>
    {/if}

  </div>
</main>

<style>
  .animate-pulse-slow {
    animation: pulse-glow 8s ease-in-out infinite;
  }
  @keyframes pulse-glow {
    0%, 100% { opacity: 0.3; transform: scale(1); }
    50% { opacity: 0.6; transform: scale(1.1); }
  }
</style>