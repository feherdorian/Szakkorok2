<template>
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
        {{ tanulo.nev
        }}<span v-if="i < tanulokCsoportja.length - 1" class="separator">,
        </span>
      </span>
    </div>
    <div v-else class="szakkor-nincs-tanulo">
      <span>Nincs beiratkozott gyerek.</span>
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
.szakkor-card {
  width: 48%;
  margin-bottom: 20px;
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

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}


.szakkor-card {
  opacity: 0;
  animation: fadeIn 0.5s forwards;
  animation-delay: 0.1s;
  transform-origin: bottom;
}


.szakkor-header,
.content-table {
  opacity: 0;
  animation: fadeIn 0.8s forwards;
  animation-delay: 0.2s;
}


.led-separator {
  opacity: 0;
  animation: fadeIn 0.5s forwards;
  animation-delay: 0.4s;
  transform-origin: bottom;
}


@keyframes glow {
  0% {
    opacity: 0.5;
  }

  100% {
    opacity: 1;
  }
}

.led-separator {
  background: linear-gradient(90deg, #4c00ff, #00bfff, #4c00ff);
  margin: 10px 0;
  border-radius: 2px;
  box-shadow: 0 0 10px rgba(76, 0, 255, 0.5), 0 0 20px rgba(0, 187, 255, 0.5);
  animation: glow 1.5s infinite alternate;
}


.szakkor-header span {
  font-size: 0.9em;
  color: #ddd;
}

.led-separator {
  width: 100%;
  height: 4px;
  background: linear-gradient(90deg,
      #4c00ff,
      #00bfff,
      #4c00ff);
  margin: 10px 0;
  border-radius: 2px;
  box-shadow: 0 0 10px rgba(76, 0, 255, 0.5), 0 0 20px rgba(0, 187, 255, 0.5);
}

.szakkor-gyerekek {
  padding-top: 10px;
}

.gyerek-nev {
  padding: 5px 0;
  color: white;
  font-size: 1.1em;
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