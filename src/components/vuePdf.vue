<template>
    <!-- Componente VuePdfApp -->
    <vue-pdf-app style="height: 100vh;" :pdf="pdfBuffer" lang="pt-BR" theme="light"/>
</template>

<script>
import VuePdfApp from "vue3-pdf-app";
import "vue3-pdf-app/dist/icons/main.css";
import { ref, onMounted } from "vue";

export default {
    components: {
        VuePdfApp,
    },
    setup() {
        // Referência para armazenar o ArrayBuffer do PDF
        const pdfBuffer = ref(null);

        // Função para carregar o PDF como ArrayBuffer
        const fetchPdf = async () => {
            try {
                // Caminho do PDF na pasta public
                const response = await fetch("../../public/028 - Política de Segurança da Informação.pdf"); // Exemplo: `public/sample.pdf`
                if (!response.ok) {
                    throw new Error("Erro ao carregar o PDF");
                }
                const arrayBuffer = await response.arrayBuffer();
                pdfBuffer.value = arrayBuffer; // Armazena o ArrayBuffer
            } catch (error) {
                console.error("Erro ao buscar o PDF:", error);
            }
        };

        // Chamar a função fetchPdf quando o componente for montado
        onMounted(() => {
            fetchPdf();
        });

        return {
            pdfBuffer,
        };
    },
};
</script>

<style scoped>
 /*.pdf-app.light {
    --pdf-toolbar-color: white;
  }*/
</style>