<script>
  import { fade, scale, fly } from "svelte/transition";
  import { cubicOut, elasticOut } from "svelte/easing";
  import { Confetti } from "svelte-confetti";
  import GradientButton from "./GradientButton.svelte";
  import { ArrowRight, Flame, WandSparkles } from "lucide-svelte";

  import "../app.css";

  // Props
  export let onNext = () => {};
  export let onDecorate = () => {};
  
  let showConfetti = false;
  let decorated = false;
  let lit = false;

  const confettiColors = ["#FF3CAC", "#F687B3", "#D8B4FE", "#C084FC", "#F472B6"];

  function decorate() {
    if (decorated) return;
    decorated = true;
    setTimeout(() => {
      onDecorate();
    }, 500);
  }

  function lightCandle() {
    if (lit) return;
    lit = true;
    showConfetti = true;
    setTimeout(() => {
      showConfetti = false;
    }, 3000);
  }
</script>

<div class="px-4 md:px-6 py-10 text-center relative min-h-[600px] flex flex-col items-center">
  
  {#if showConfetti}
    <div class="fixed top-[60%] left-1/2 -translate-x-1/2 -translate-y-1/2 z-50 pointer-events-none">
      <Confetti 
        x={[-1.5, 1.5]} 
        y={[-1.5, 1.5]} 
        amount={200} 
        delay={[0, 500]}
        fallDistance="60vh"
        colorArray={confettiColors}
      />
    </div>
  {/if}

  {#if lit}
    <div 
      in:fly={{ y: 50, duration: 1000, delay: 1500, easing: cubicOut }}
      class="fixed top-32 md:top-40 left-0 w-full text-center px-4 z-20 pointer-events-none"
    >
      <h1 
        class="text-[40px] md:text-6xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-violet-400 via-fuchsia-400 to-pink-400 leading-tight"
        style="filter: drop-shadow(0 0 20px rgba(255,105,180,0.4));"
      >
        Feliz Cumpleaños, Preciosa!
      </h1>
    </div>
  {/if}

  <div class="relative flex flex-col items-center gap-8 mt-40 md:mt-52 w-full">
    
    <!-- EL PASTEL -->
    <div class="relative mb-6">
      <div class="cake">
        <div class="plate"></div>
        <div class="layer layer-bottom"></div>
        <div class="layer layer-middle"></div>
        <div class="layer layer-top"></div>
        <div class="icing"></div>
        <div class="drip drip1"></div>
        <div class="drip drip2"></div>
        <div class="drip drip3"></div>
        
        <div class="candle">
          {#if lit}
            <div 
              in:scale={{ duration: 900, start: 0.2, easing: elasticOut }}
              class="flame"
            ></div>
          {/if}
        </div>
      </div>
    </div>

    <div class="h-16 relative w-full flex justify-center items-center">
      {#if !lit}
        <div 
          in:scale={{ duration: 500, delay: 500 }}
          out:scale={{ duration: 400, opacity: 0 }}
          class="absolute"
        >
          <GradientButton onClick={lightCandle}>
            <Flame size={20} />
            Encender Vela
          </GradientButton>
        </div>
      {:else}
        <div 
          in:scale={{ duration: 500, delay: 2000, easing: cubicOut }}
          class="absolute"
        >
          <GradientButton onClick={onNext}>
            Continuar
            <ArrowRight size={20} class="mt-0.5" />
          </GradientButton>
        </div>
      {/if}
    </div>

  </div>
</div>