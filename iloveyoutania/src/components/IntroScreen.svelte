<script>
  import GradientButton from "./GradientButton.svelte";
  import { Gift } from "lucide-svelte";
  import { ArrowRight, Flame, WandSparkles } from "lucide-svelte";

  // Recibimos la función onNext
  export let onNext = () => {};
</script>

<div class="py-10 md:py-14 text-center">
  <div class="flex flex-col items-center gap-6">
    <img
      src="https://i.pinimg.com/originals/50/ed/9d/50ed9d33c7e610ea977cf47a6a58ee9b.gif"
      alt="Cute birthday animation"
      class="w-[140px] md:w-[180px] object-cover"
    />

    <div>
      <h1 
        class="text-pretty text-4xl md:text-6xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-violet-400 via-fuchsia-400 to-pink-400 drop-shadow leading-tight"
        style="filter: drop-shadow(0 0 20px rgba(255,105,180,0.4));"
      >
        ¡La Más Grande Maravilla nació hoy, hace 22 años!
      </h1>
      <p class="mt-4 text-xl text-pink-200">
        Y sí, ¡eres TÚ! La razón por la que hoy es un día extraordinario.
      </p>
    </div>

<div class="mt-8">
  <GradientButton 
    onClick={onNext} 
    className="bg-white text-black px-6 py-3 rounded-full font-bold z-50 relative hover:bg-gray-200 transition"
  >
    CONTINUAR
    <ArrowRight size={20} class="mt-0.5" />
  </GradientButton>
</div>
  </div>
</div>