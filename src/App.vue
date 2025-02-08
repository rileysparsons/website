<script setup lang="ts">
import { ref, useTemplateRef } from 'vue';

const isExpanded = ref(false);
const popoverContent = useTemplateRef('popoverContent');

const expandContent = (id: string) => {
  if (id === 'transcripta') {
    isExpanded.value = !isExpanded.value;
  }
};

function handleOutsideClick(event) {
  console.log(event.target, popoverContent.valu);
  if (popoverContent.value && !popoverContent.value.contains(event.target)) {
    isExpanded.value = false;
  }
};

</script>

<template>
  <main>
    <div id='name'>Riley Parsons</div>
    <section>
      <p>As the first engineer at <a href="https://www.transcriptabio.com/">Transcripta Bio</a>, I designed and built <a href="#transcripta-detail" @click.prevent="() => expandContent('transcripta')">software</a> to accelerate drug discovery research.</p>
      
      <div v-if="isExpanded" class="popover" @click="handleOutsideClick">
        <div ref="popoverContent" class="popover-content">
          <div v-if="isExpanded" class="feature" id="expanded">
            <video controls autoplay>
              <source src="@/assets/atlas_explorer_transcripta.mp4" type="video/mp4" />
              Your browser does not support the video tag.
            </video>
            <p>Atlas Explorer powers drug discovery at Transcripta Bio, helping scientists quickly analyze and share drug-gene response data alongside validation assays and key metadata.</p>
          </div>
        </div>
      </div>
      
      <transition name="expand">

      </transition>
      <p>Before that, I worked at <a href="https://www.ionpath.com/">Ionpath</a>, focusing on instrument control software for a high-resolution digital pathology instrument.</p>
    </section>
  </main>
</template>

<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400..900;1,400..900&display=swap');

  #name {
    font-size: 2rem;
    font-weight: bold;
    font-family: 'Playfair Display', serif;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  section p {
    margin: 1rem 0;
  }

  section {
    margin: 3rem 0;
  }

  .feature video {
    width: 800px;
    height: auto;
  }

  .popover-content {
    display: inline-block;
  }

  .popover-content p {
    width: 800px;
  }

  /* Popover styling */
  .popover {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: rgba(0, 0, 0, 0.6);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
  }
</style>
