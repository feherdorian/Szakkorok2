<template>
  <div class="szakkor-card animacio" style="animation-delay: 2s">
    <div class="szakkor-header">
      <h2>{{ szakkor.nev }}</h2>
      <span>
        (Tagok: <span class="tagokSzama">{{ tanulokCsoportja.length }}</span
        >)
      </span>
    </div>

    <div class="led-separator"></div>
    <!-- LED-stílusú elválasztó vonal -->

    <div v-if="tanulokCsoportja.length > 0" class="szakkor-gyerekek">
      <span
        v-for="(tanulo, i) in tanulokCsoportja"
        :key="tanulo.id"
        class="gyerek-nev"
      >
        {{ tanulo.nev
        }}<span v-if="i < tanulokCsoportja.length - 1" class="separator"
          >,
        </span>
      </span>
    </div>
    <div v-else class="szakkor-nincs-tanulo">
      <span>Nincs beiratkozott gyerek.</span>
      <!-- Ha nincs beiratkozott gyerek, ezt jelenítjük meg -->
    </div>
  </div>
</template>
  
  <script>
export default {
  props: ["szakkor", "tanulok"], // A szakkör és a tanulók átadása propokként
  computed: {
    tanulokCsoportja() {
      // Visszaadja a szakkörhöz tartozó tanulókat, rendezve név szerint
      return this.tanulok
        .filter((t) => t.szakkorId == this.szakkor.id) // Szűrés a szakkör ID-ja alapján
        .sort((a, b) => a.nev.localeCompare(b.nev)); // Név szerinti rendezés
    },
  },
};
</script>
  
  <style scoped>
.szakkor-card {
  border: 1px solid #ccc; /* Határ a kártyán */
  border-radius: 8px; /* Lekerekített sarkok */
  padding: 20px; /* Növelt belső tér a jobb elhelyezés érdekében */
  width: 100%; /* A kártya szélessége */
  background-color: #282828; /* Sötét háttér a kártyán */
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3); /* Árnyék a mélység érdekében */
  color: var(--color); /* Szöveg színének beállítása */
  transition: box-shadow 0.3s; /* Átmenet az árnyék megváltoztatásakor */
}

.szakkor-card:hover {
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.4); /* Erősebb árnyék az egérmutató fölé helyezésekor */
}

.szakkor-header {
  display: flex; /* Flexbox elrendezés */
  justify-content: space-between; /* Terjedjön el a tér a fejlécelemek között */
  align-items: center; /* Középre igazítja az elemeket */
  padding-bottom: 10px; /* Tér alul a fejléc alatt */
  margin-bottom: 10px; /* Tér a fejléc és a tartalom között */
  border-bottom: 2px solid var(--color); /* Alsó határ a fejlécnél */
}

.szakkor-header h2 {
  margin: 0; /* Törölje a margin-t a h2 címnél */
  font-size: 1.5em; /* Cím mérete */
  color: var(--color); /* Cím színe */
}
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px); /* Slight slide-up effect */
  }
  to {
    opacity: 1;
    transform: translateY(0); /* Move to original position */
  }
}

/* Animation applied to the szakkor card box */
.szakkor-card {
  opacity: 0; /* Initially invisible */
  animation: fadeIn 0.5s forwards; /* Fade-in with slide-up effect */
  animation-delay: 0.1s; /* Appear earlier than the LED */
  transform-origin: bottom; /* Origin of the transformation */
}

/* Sync header and content with the card */
.szakkor-header,
.content-table {
  opacity: 0;
  animation: fadeIn 0.5s forwards; /* Apply fade-in animation */
  animation-delay: 0.2s; /* Slightly delayed from the box */
}

/* LED separator animation - delay more than the card */
.led-separator {
  opacity: 0;
  animation: fadeIn 0.5s forwards;
  animation-delay: 0.4s; /* LEDs appear after the card and content */
  transform-origin: bottom; /* Same effect with slight delay */
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
  font-size: 0.9em; /* Kis méret a tagok számának */
  color: #ddd; /* Szürke szín a tagok számának */
}

.led-separator {
  width: 100%; /* Teljes szélesség */
  height: 4px; /* LED vonal vastagsága */
  background: linear-gradient(
    90deg,
    #4c00ff,
    #00bfff,
    #4c00ff
  ); /* LED-stílusú gradient háttér */
  margin: 10px 0; /* Tér a vonal felett és alatt */
  border-radius: 2px; /* Lekerekített sarkok */
  box-shadow: 0 0 10px rgba(76, 0, 255, 0.5), 0 0 20px rgba(0, 187, 255, 0.5); /* Glowing hatás */
}

.szakkor-gyerekek {
  padding-top: 10px; /* Tér a gyerekek lista felett */
}

.gyerek-nev {
  padding: 5px 0; /* Tér a gyereknevek között */
  color: var(--color); /* Gyerek név színe */
  font-size: 1.1em; /* Méret megtartása */
}

.separator {
  color: #000 !important; /* Elválasztó szín */
}

.szakkor-nincs-tanulo {
  font-style: italic; /* Dőlt betű stílus */
  color: #ccc; /* Világosabb szín a "nincs tanuló" üzenethez */
}

.tagokSzama {
  color: var(--color); /* Tagok számának színe */
  font-weight: bold; /* Félkövér a tagok számának kiemelésére */
}
</style>
  