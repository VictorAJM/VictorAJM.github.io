<script>
  import { fly } from "svelte/transition";
  import GradientButton from "./GradientButton.svelte";
  import { ArrowRight } from "lucide-svelte";

  // Props
  export let onNext = () => {};
</script>

<div class="px-4 md:px-6 py-10 text-center flex flex-col items-center">
  
  <!-- Título con animación de entrada -->
  <h2
    in:fly={{ y: 20, duration: 800 }}
    class="text-3xl md:text-5xl font-semibold text-transparent bg-clip-text bg-gradient-to-r from-pink-400 via-fuchsia-400 to-purple-400 drop-shadow mb-6 leading-tight"
  >
    Un mensaje especial para ti
  </h2>

  <div class="mx-auto relative w-full max-w-3xl flex justify-center flex-col items-center gap-8">
    
    <div
      in:fly={{ y: 30, duration: 1000, delay: 200 }}
      class="h-auto max-w-xl bg-gradient-to-br from-pink-200 via-pink-100 to-pink-50 rounded-2xl shadow-lg p-6 md:p-8 text-center"
    >
      <p class="text-[#301733] text-base md:text-lg leading-relaxed whitespace-pre-line">
        ¡Feliz cumpleaños, hermosa!

        Hoy, 25 de noviembre, toca celebrar a la persona que, sin proponérselo ni darse cuenta, ilumina todo lo que toca, mejora cada lugar al que va y hace que el mundo sea un lugar mejor.

        Tienes una manera muy especial de hacer que los días y la vida se sientan más ligeros y tranquilos. Tu voz, que transmite paz y energía; tu sonrisa, que brinda alegría en cualquier ambiente y situación; tus ojos hermosos, que cautivan a todos; y tu forma tan única de ser, que deja huella en cualquiera que te llega a conocer.

        No te lo digo desde una posición romántica, sino como alguien que ha visto cosas en ti y que se siente muy afortunado de conocerte. Siéndote completamente sincero, me atrevo a afirmar que eres especial. Muy especial. Eres la clase de persona cuya presencia mejora el mundo: haces la diferencia entre todas las personas, tu energía mueve, inspira y hace que todo alrededor se sienta mejor.

        Ojalá que en este cumpleaños se te pueda regresar un poco de todo lo que haces por el mundo. Deseo con todo el corazón que seas muy feliz hoy, que sea un día tranquilo y divertido, y que sigas teniendo, hoy y siempre, mil motivos para sonreír y cumplir todas tus metas y sueños. Sigue brillando con toda la intensidad del mundo, Selene.

        Te deseo siempre lo mejor. En este mundo y en esta vida, solo quiero que seas tan feliz como te sea posible. Te tengo algunas sorpresitas para ayudar a que eso ocurra, al ratito las verás jejeje. Con esto, solo busco hacerte sentir algo bonito, solo quiero que veas lo increíble que eres y que puedas sentir lo que me haces sentir siempre.

        Feliz cumpleaños, Tania, la más grande Maravilla. 💗

        Con mucho cariño y con toda el alma. Te quiere, tu osito.
      </p>
    </div>


  </div>
</div>