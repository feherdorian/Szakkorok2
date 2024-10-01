<template>
  <div class="row">
    <div class="col-md-6 side-a">
      <h1 class="table-title">Táblázat</h1> <!-- A táblázat címe -->
      <div class="led-separator2"></div> <!-- LED-stílusú elválasztó vonal -->
      <table class="content-table animacio" style="animation-delay: 1s">
        <thead>
          <tr>
            <th>Név</th> <!-- Tanuló neve -->
            <th>Osztály</th> <!-- Tanuló osztálya -->
            <th>Szakkör</th> <!-- Szakkör kiválasztása -->
          </tr>
        </thead>
        <tbody>
          <tr v-for="(tanulo, i) in tanulok" :key="i">
            <td class="table-cell">
              <span class="icon">
                <!-- Person Icon SVG -->
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-person" viewBox="0 0 16 16">
                  <path d="M3 14s-1 0-1-1 1-1 1-1h10s1 0 1 1-1 1-1 1H3zm8-9a3 3 0 1 0-6 0 3 3 0 0 0 6 0z"/>
                </svg>
              </span>
              {{ tanulo.nev }}
            </td> <!-- Tanuló neve -->
            <td class="table-cell">{{ tanulo.osztaly }}</td> <!-- Tanuló osztálya -->
            <td class="table-cell">
              <select v-model="tanulo.szakkorId" class="select"> <!-- Szakkör kiválasztására szolgáló legördülő lista -->
                <option v-for="(szakkor, i) in szakkorok" :key="i" :value="szakkor.id">
                  {{ szakkor.nev }} <!-- Szakkör neve -->
                </option>
              </select>
            </td>
          </tr>
        </tbody>
      </table>
      <div class="led-separator"></div> <!-- LED-stílusú elválasztó vonal -->
    </div>
    
    <div class="col-md-6 side-b">
      <div class="szakkor-lista">
        <GyerekLista
          v-for="szakkor in szakkorok"
          :key="szakkor.id"
          :szakkor="szakkor"    
          :tanulok="tanulok" 
        />
      </div>
    </div>
  </div>
</template>

<script>
import GyerekLista from "../components/Gyereklista.vue"; // GyerekLista komponens importálása

export default {
  components: {
    GyerekLista, // A GyerekLista komponenst regisztráljuk
  },
  data() {
    return {
      // Tanulók listája
      tanulok: [
        { id: 1, nev: "Erős Pista", osztaly: "3a", szakkorId: 1 },
        { id: 2, nev: "Gyenge Pista", osztaly: "7b", szakkorId: 1 },
        { id: 3, nev: "Kis Pista", osztaly: "1a", szakkorId: 1 },
        { id: 4, nev: "Ledacs-Kiss Pista", osztaly: "8a", szakkorId: 1 },
        { id: 5, nev: "Tóth Pista", osztaly: "4c", szakkorId: 1 },
        { id: 6, nev: "Magyar Pista", osztaly: "9c", szakkorId: 1 },
        { id: 7, nev: "Német Pista", osztaly: "10b", szakkorId: 1 },
      ],
      // Szakkörök listája
      szakkorok: [
        { id: 1, nev: "Nincs szakkör" },
        { id: 2, nev: "Informatika" },
        { id: 3, nev: "Rajz" },
        { id: 4, nev: "Ének" },
        { id: 5, nev: "Kosárlabda" },
        { id: 6, nev: "Football" },
      ],
    };
  },
};
</script>

<style scoped>
.table-title {
  font-size: 2em; /* Cím betűmérete */
  color: var(--color); /* Cím színe */
  text-align: center; /* Cím középre igazítása */
  margin-bottom: 20px; /* Tér a cím alatt */
  text-shadow: 
    0 0 5px rgba(76, 0, 255, 0.8), /* Lila fényesség */
    0 0 10px rgba(0, 187, 255, 0.6); /* Kék fényesség */
}
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px); /* Enyhén lejjebb mozgás */
  }
  to {
    opacity: 1;
    transform: translateY(0); /* Eredeti pozíció */
  }
}

.table-title,
.led-separator,
.led-separator2,
.content-table {
  opacity: 0; /* Kezdetben láthatatlan */
  animation: fadeIn 0.5s forwards; /* Fade-in animáció */
}

.table-title {
  animation-delay: 0.2s; /* Késleltetés a címnél */
}

.led-separator {
  animation-delay: 0.6s; /* Késleltetés az első LED elválasztónál */
}

.led-separator2 {
  animation-delay: 0.8s; /* Késleltetés a második LED elválasztónál */
}

.content-table {
  animation-delay: 0.4s; /* Késleltetés a táblázatnál */
}

@keyframes glow {
  0% {
    opacity: 0.5; /* Kezdeti fényesség */
  }
  100% {
    opacity: 1; /* Maximális fényesség */
  }
}

.content-table {
  border-collapse: collapse; /* Határok összevonása */
  margin: 25px 0; /* Margó a táblázat körül */
  font-size: 1em; /* Betűméret az olvashatóság érdekében */
  min-width: 800px; /* Minimális szélesség */
  border-radius: 10px; /* Lekerekített sarkok */
  overflow: hidden; /* Túlfolyás elrejtése */
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3); /* Árnyék a táblázat körül */
}

.content-table thead tr {
  background-color: var(--color); /* Fejléc háttérszíne */
  color: #ffffff; /* Fejléc szöveg színe */
  text-align: left; /* Fejléc szöveg balra igazítása */
  font-weight: bold; /* Fejléc szöveg félkövér */
}


.content-table th,
.content-table td {
  padding: 12px 15px; /* Cellák közötti tér */
}

.content-table tbody tr {
  border-bottom: 1px solid rgba(255, 255, 255, 0.1); /* Alul határ a sorok között */
  transition: background-color 0.3s; /* Átmenet az effektusokhoz */
  background-color: rgba(255, 255, 255, 0.05); /* Háttérszín a sorokhoz */
}

.content-table tbody tr:hover {
  background-color: rgba(255, 255, 255, 0.1); /* Hover effektus a sorokhoz */
}

.content-table tbody tr:nth-of-type(even) {
  background-color: rgba(255, 255, 255, 0.02); /* Páros sorok háttérszíne */
}

.table-cell {
  color: var(--color); /* Szöveg színe a cellákban */
  font-weight: 500; /* Szöveg súlya */
  border: 1px solid rgba(255, 255, 255, 0.1); /* Cellák határai */
  border-radius: 5px; /* Lekerekített sarkok */
  background-color: rgba(255, 255, 255, 0.1); /* Cellák háttérszíne */
  transition: background-color 0.3s ease; /* Háttérszín átmenet */
}

.table-cell:hover {
  background-color: rgba(255, 255, 255, 0.2); /* Cellák háttérszínének változása hover esetén */
}

.icon {
  display: inline-block; /* Inline blokk az ikon számára */
  margin-right: 5px; /* Tér a név és az ikon között */
  vertical-align: middle; /* Középre igazítás vertikálisan */
}

.select {
  padding: 6px 10px; /* Padding a legördülő listához */
  border: 1px solid var(--color); /* Határ színe a legördülő listához */
  border-radius: 5px; /* Lekerekített sarkok */
  background-color: rgba(255, 255, 255, 0.1); /* Háttérszín */
  color: var(--color); /* Szöveg színe */
  transition: background-color 0.3s; /* Háttérszín átmenet */
}

.select:hover {
  background-color: rgba(255, 255, 255, 0.2); /* Hover effektus a legördülő listához */
}

.led-separator {
  height: 5px; /* Elválasztó vonal magassága */
  width: 90%; /* Szélesség */
  margin: 20px 0; /* Tér az elválasztó körül */
  background: linear-gradient(90deg, #4c00ff, #00bfff, #4c00ff); /* LED-szerű hatás */
  border-radius: 5px; /* Lekerekített sarkok */
  box-shadow: 0 0 10px rgba(76, 0, 255, 0.5), 0 0 20px rgba(0, 187, 255, 0.5); /* Fényhatás */
  animation: glow 1.5s infinite alternate; /* Pulzáló animáció */
}

.led-separator2 {
  height: 5px; /* Második elválasztó vonal magassága */
  width: 20%; /* Szélesség */
  margin: 2px auto; /* Középre igazítva, kis margóval */
  background: linear-gradient(90deg, #4c00ff, #00bfff, #4c00ff); /* LED-szerű hatás */
  border-radius: 5px; /* Lekerekített sarkok */
  animation: glow 1.5s infinite alternate; /* Pulzáló animáció */
  box-shadow: 0 0 10px rgba(76, 0, 255, 0.5), 0 0 20px rgba(0, 187, 255, 0.5); /* Fényhatás */
}
</style>
