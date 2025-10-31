<template>
    <div class="contextmenu-wrapper" @click="hideMenu">
        <slot />

        <div 
        v-if="visible" 
        class="contextmenu" 
        :style="{ top: `${y}px`, left: `${x}px` }"
        >
        {{ definition }}
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue';

const visible = ref(false);
const x = ref(0);
const y = ref(0);
const definition = ref<string | null>(null)

let currentWord = '';

function getSelectedWord(_event: MouseEvent): string {
    const selection = window.getSelection()?.toString().trim() || '';
    return selection.split(/\s+/)[0] || '';
}

async function getDefinition(mot: string) {
    definition.value = 'Chargement...'
    try {
        const response = await fetch(`https://en.wiktionary.org/api/rest_v1/page/definition/${mot}`);
        const data = await response.json();
        if (data.fr && Array.isArray(data.fr) && data.fr.length > 0) {
            const defs = data.fr.flatMap((entry: { definitions: { definition: string }[] }) =>
            entry.definitions
        );

        const cleanDefs = defs.map((d: { definition: string }) =>
            d.definition.replace(/<[^>]+>/g, '')
        )

        definition.value = cleanDefs.join('\n')
        } else {
            definition.value = 'Aucune définition française trouvée.'
        }
    } catch (err) {
        definition.value = 'Erreur lors de la récupération';
    }
}

function onContextMenu(event: MouseEvent) {
    event.preventDefault();

    currentWord = getSelectedWord(event);
    if (!currentWord) return;

    x.value = event.clientX;
    y.value = event.clientY;
    visible.value = true;

    getDefinition(currentWord);
}

function hideMenu() {
    visible.value = false;
}

onMounted(() => {
    document.addEventListener('contextmenu', onContextMenu);
});
onBeforeUnmount(() => {
    document.removeEventListener('contextmenu', onContextMenu);
});
</script>

<style scoped>
.contextmenu {
  position: absolute;
  background-color: white;
  color: black;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 12px;
  border-radius: 4px;
  border: 1px solid #dcdfe6;
  padding: 1rem;
  z-index: 1000;
  min-width: 200px;
  max-width: 300px;
  word-break: break-word;
}
</style>
