<script lang="ts">
    import { originalImage, modifiedImage } from "./store";
    import 'two-up-element';

    let processingImage = true;
    let tries = 0;
    let intervalId: any;

    $:{
        if(processingImage){
            clearInterval(intervalId)
            intervalId = setInterval(() => {
                tries++;
            }, 500);
        }
    }
</script>

<two-up>
    <img src={$originalImage} alt="Imagen original del usuario">
    <img
    on:load={() => (processingImage = false)}
    on:error={() => (processingImage = true)}
    src={`${$modifiedImage}&t=${tries}`} 
    alt="Imagen sin fondo del usuario">
</two-up>

<a download href={$modifiedImage} class="block mt-10 bg-blue-500 text-xl hover:bg-blue-700 text-center w-full font-bold text-white rounded-full px-4 py-2">Descargar imagen sin fondo</a>