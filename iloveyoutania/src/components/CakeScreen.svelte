<script>
  import { scale, fly, fade } from "svelte/transition";
  import { elasticOut, cubicOut } from "svelte/easing";
  
  // 1. Cambia la importación
  import { Confetti } from "svelte-confetti";
  
  import GradientButton from "./GradientButton.svelte";
  import { ArrowRight, Flame } from "lucide-svelte";

  export let onNext = () => {};
  export let onDecorate = () => {};

  let decorated = false;
  let lit = false;
  
  // Colores convertidos para svelte-confetti
  const confettiColors = ["#FF3CAC", "#F687B3", "#D8B4FE", "#C084FC", "#F472B6"];

  const decorate = () => {
    if (decorated) return;
    decorated = true;
    setTimeout(() => {
      onDecorate?.();
    }, 500);
  };

  const lightCandle = () => {
    if (lit) return;
    // 2. Simplemente activamos el estado 'lit'. 
    // El HTML reaccionará mostrando el componente de confeti.
    lit = true;
  };
</script>

<div class="px-4 md:px-6 py-10 text-center relative min-h-screen overflow-hidden">

  {#if lit}
    <div style="position: fixed; top: 60%; left: 50%; transform: translate(-50%, -50%); pointer-events: none; z-index: 100;">
      <Confetti 
        x={[-1, 1]} 
        y={[-1, 1]} 
        amount={140} 
        colorArray={confettiColors} 
        fallDistance="100vh"
        duration={3000}
      />
    </div>
  {/if}

  {#if lit}
    <div
      in:fly={{ y: 50, duration: 1000, delay: 1500, easing: cubicOut }}
      class="fixed top-32 lg:top-40 left-0 w-full text-center text-[40px] md:text-6xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-violet-400 via-fuchsia-400 to-pink-400 drop-shadow leading-tight px-4 z-50"
      style="filter: drop-shadow(0 0 20px rgba(255,105,180,0.4));"
    >
      Happy Birthday, Cutiepie!
    </div>
  {/if}

  <div class="relative flex flex-col items-center gap-8 mt-52">
     <div class="relative mb-6 transform scale-125 md:scale-150">
        <div class="cake">
            <div class="candle">
              {#if lit}
                <div in:scale={{ duration: 900, start: 0.2, easing: elasticOut }} class="flame"></div>
              {/if}
            </div>
        </div>
     </div>

    <div class="h-16 flex items-center justify-center">
      {#if !lit}
        <div out:scale={{ duration: 300, start: 0.8 }} in:scale={{ duration: 500, delay: 500, start: 0.8 }} class="absolute">
          <GradientButton on:click={lightCandle}>
            <div class="flex items-center gap-2">
              <Flame size={20} />
              <span>Light the Candle</span>
            </div>
          </GradientButton>
        </div>
      {:else}
        <div in:scale={{ duration: 500, delay: 2000, start: 0.8 }} class="absolute">
          <GradientButton on:click={onNext}>
             <div class="flex items-center gap-2">
              <span>Next</span>
              <ArrowRight size={20} class="mt-0.5" />
            </div>
          </GradientButton>
        </div>
      {/if}
    </div>
  </div>
</div>

<style>
  /* --- ESTILOS DEL PASTEL (CSS CAKE) --- */
  .cake {
    position: relative;
    width: 250px;
    height: 200px;
    display: flex;
    justify-content: center;
    align-items: flex-end;
  }

  .plate {
    position: absolute;
    bottom: 0;
    width: 270px;
    height: 10px;
    background-color: #e2e8f0;
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }

  .layer {
    position: absolute;
    background-color: #fce7f3; /* Pink-100 base */
    border-radius: 10px;
    border: 2px solid #fbcfe8; /* Pink-200 border */
  }

  .layer-bottom {
    bottom: 10px;
    width: 220px;
    height: 50px;
    background-color: #fbcfe8; /* Pink-200 */
  }

  .layer-middle {
    bottom: 60px;
    width: 180px;
    height: 50px;
    background-color: #f9a8d4; /* Pink-300 */
    z-index: 2;
  }

  .layer-top {
    bottom: 110px;
    width: 140px;
    height: 50px;
    background-color: #f472b6; /* Pink-400 */
    z-index: 3;
  }

  .icing {
    position: absolute;
    bottom: 160px;
    width: 140px;
    height: 15px;
    background-color: #fff;
    border-radius: 10px 10px 5px 5px;
    z-index: 4;
  }

  .drip {
    position: absolute;
    background-color: #fff;
    width: 15px;
    height: 25px;
    border-radius: 0 0 10px 10px;
    z-index: 4;
    bottom: 145px; /* Adjust based on icing */
  }

  .drip1 { left: 70px; height: 30px; }
  .drip2 { left: 100px; height: 20px; }
  .drip3 { left: 130px; height: 35px; }

  .candle {
    position: absolute;
    bottom: 160px;
    left: 50%;
    transform: translateX(-50%);
    width: 12px;
    height: 40px;
    background: repeating-linear-gradient(
      45deg,
      #fff,
      #fff 5px,
      #f472b6 5px,
      #f472b6 10px
    );
    z-index: 5;
    border-radius: 4px;
  }

  .flame {
    position: absolute;
    top: -20px;
    left: 50%;
    transform: translateX(-50%);
    width: 16px;
    height: 24px;
    background-color: #fbbf24; /* Amber */
    border-radius: 50% 50% 20% 20%;
    box-shadow: 
      0 0 10px #fbbf24,
      0 0 20px #f59e0b,
      0 0 40px #fff;
    animation: flicker 1s infinite alternate;
    transform-origin: bottom center;
  }

  @keyframes flicker {
    0% { transform: translateX(-50%) scale(1); opacity: 0.9; }
    100% { transform: translateX(-50%) scale(1.1); opacity: 1; }
  }
</style>