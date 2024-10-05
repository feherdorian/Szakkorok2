<template>  
  <div class="szakkorok-container">
    <div class="szakkor-card animacio" style="animation-delay: 2s">
      <div class="szakkor-header">
        <h2>{{ szakkor.nev }}</h2>
        <span>
          (Tagok: <span class="tagokSzama">{{ tanulokCsoportja.length }}</span>)
        </span>
      </div>

      <div class="led-separator"></div>

      <div v-if="tanulokCsoportja.length > 0" class="szakkor-gyerekek">
        <span v-for="(tanulo, i) in tanulokCsoportja" :key="tanulo.id" class="gyerek-nev">
          {{ tanulo.nev }}<span v-if="i < tanulokCsoportja.length - 1" class="separator">, </span>
        </span>
      </div>
      <div v-else class="szakkor-nincs-tanulo">
        <span>Nincs beiratkozott gyerek.</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["szakkor", "tanulok"],
  computed: {
    tanulokCsoportja() {
      return this.tanulok
        .filter((t) => t.szakkorId == this.szakkor.id)
        .sort((a, b) => a.nev.localeCompare(b.nev));
    },
  },
};
</script>

<style scoped>
.szakkorok-container {
  display: flex;
  justify-content: flex-end; 
  flex-wrap: wrap;
  padding: 20px;
}

.szakkor-card {
  width: 100%; 
  max-width: 400px; 
  margin: 10px; 
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 20px;
  background-color: #282828;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
  color: var(--color);
  transition: box-shadow 0.3s;
}

.szakkor-card:hover {
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.4);
}

.szakkor-header {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.szakkor-header h2 {
  margin: 0;
  font-size: 1.5em;
  color: white;
}


@media (max-width: 600px) {
  .szakkorok-container {
    justify-content: center; 
  }
  .szakkor-card {
    padding: 15px;
  }
  .szakkor-header h2 {
    font-size: 1.3em;
  }
  .gyerek-nev {
    font-size: 1em;
    flex: 1 1 100%;
  }
}


.led-separator {
  background: linear-gradient(90deg, #4c00ff, #00bfff, #4c00ff);
  margin: 10px 0;
  border-radius: 2px;
  box-shadow: 0 0 10px rgba(76, 0, 255, 0.5), 0 0 20px rgba(0, 187, 255, 0.5);
  animation: glow 1.5s infinite alternate;
}

@keyframes glow {
  0% {
    opacity: 0.5;
  }
  100% {
    opacity: 1;
  }
}


.szakkor-gyerekek {
  padding-top: 10px;
  display: flex;
  flex-wrap: wrap;
}

.gyerek-nev {
  padding: 4px;
  color: white;
}

.separator {
  color: #000 !important;
}

.szakkor-nincs-tanulo {
  font-style: italic;
  color: #ccc;
}

.tagokSzama {
  color: var(--color);
  font-weight: bold;
}
</style>
