<template>
  <div class="row">
    <div class="col-md-6 col-12 side-a">
      <h1 class="table-title">Táblázat</h1>
      <div class="led-separator2"></div>
      <table class="content-table animacio" style="animation-delay: 1s">
        <thead>
          <tr>
            <th>Név</th>
            <th>Osztály</th>
            <th>Szakkör</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(tanulo, i) in tanulok" :key="i">
            <td class="table-cell">
              <span class="icon">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="16"
                  height="16"
                  fill="currentColor"
                  class="bi bi-person"
                  viewBox="0 0 16 16"
                  :style="{ color: getIconColor(tanulo.nev) }" 
                >
                  <path
                    d="M3 14s-1 0-1-1 1-1 1-1h10s1 0 1 1-1 1-1 1H3zm8-9a3 3 0 1 0-6 0 3 3 0 0 0 6 0z"
                  />
                </svg>
              </span>
              {{ tanulo.nev }}
            </td>
            <td class="table-cell">{{ tanulo.osztaly }}</td>
            <td class="table-cell">
              <select v-model="tanulo.szakkorId" class="select">
                <option
                  v-for="(szakkor, i) in szakkorok"
                  :key="i"
                  :value="szakkor.id"
                >
                  {{ szakkor.nev }}
                </option>
              </select>
            </td>
          </tr>
        </tbody>
      </table>
      <div class="led-separator"></div>
    </div>

    <div class="col-md-6 col-12 side-b">
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
import GyerekLista from "../components/Gyereklista.vue";

export default {
  components: {
    GyerekLista,
  },
  data() {
    return {
      tanulok: [
        { id: 1, nev: "Erős Anna ", osztaly: "3a", szakkorId: 1 },
        { id: 2, nev: "Gyenge Julianna", osztaly: "7b", szakkorId: 1 },
        { id: 3, nev: "Kis Pista", osztaly: "1a", szakkorId: 1 },
        { id: 4, nev: "Ledacs-Kiss Pista", osztaly: "8a", szakkorId: 1 },
        { id: 5, nev: "Tóth Margit", osztaly: "4c", szakkorId: 1 },
        { id: 6, nev: "Magyar Pista", osztaly: "9c", szakkorId: 1 },
        { id: 7, nev: "Német Erzsébet", osztaly: "10b", szakkorId: 1 },
      ],

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
  methods: {
    getIconColor(name) {
      const girlNames = ["Anna", "Julianna", "Margit", "Erzsébet"]; 
      return girlNames.some(girlName => name.includes(girlName)) ? "pink" : "blue";
    },
  },
};
</script>


<style scoped>
.table-title {
  font-size: 2em;
  color: var(--color);
  text-align: center;
  margin-bottom: 20px;
  text-shadow: 0 0 5px rgba(76, 0, 255, 0.8), 0 0 10px rgba(0, 187, 255, 0.6);
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

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateX(-100%);
  }

  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.table-title,
.led-separator,
.led-separator2,
.content-table {
  opacity: 0;
  animation: fadeIn 0.5s forwards;
}

.table-title {
  animation-delay: 0.2s;
}

.led-separator {
  animation-delay: 0.4s;
}

.led-separator2 {
  animation-delay: 0.6s;
}

.content-table {
  animation: slideIn 0.8s bounce-in;
  animation-delay: 1s;
}

@keyframes glow {
  0% {
    opacity: 0.5;
  }

  100% {
    opacity: 1;
  }
}

.content-table {
  border-collapse: collapse;
  margin: 25px 0;
  font-size: 1em;
  min-width: 800px;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
}

.content-table thead tr {
  background-color: var(--color);
  color: #ffffff;
  text-align: left;
  font-weight: bold;
}

.content-table th,
.content-table td {
  padding: 12px 15px;
}

.content-table tbody tr {
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  transition: background-color 0.3s;
  background-color: rgba(255, 255, 255, 0.05);
}

.content-table tbody tr:hover {
  background-color: rgba(255, 255, 255, 0.1);
}

.content-table tbody tr:nth-of-type(even) {
  background-color: rgba(255, 255, 255, 0.02);
}

.table-cell {
  color: white;
  font-weight: 500;
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 5px;
  background-color: rgba(255, 255, 255, 0.1);
  transition: background-color 0.3s ease;
}

.table-cell:hover {
  background-color: rgba(255, 255, 255, 0.2);
}

.icon {
  display: inline-block;
  margin-right: 5px;
  vertical-align: middle;
  color: var(--color);
}

.select {
  padding: 6px 10px;
  border: 1px solid var(--color);
  border-radius: 5px;
  background-color: rgba(255, 255, 255, 0.1);
  color: white;
  transition: background-color 0.3s;
}

.select:hover {
  background-color: var(--color);
}

.led-separator {
  height: 5px;
  width: 90%;
  margin: 20px 0;
  background: linear-gradient(90deg, #4c00ff, #00bfff, #4c00ff);
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(76, 0, 255, 0.5), 0 0 20px rgba(0, 187, 255, 0.5);
  animation: glow 1.5s infinite alternate;
}

.led-separator2 {
  height: 5px;
  width: 20%;
  margin: 2px auto;
  background: linear-gradient(90deg, #4c00ff, #00bfff, #4c00ff);
  border-radius: 5px;
  animation: glow 1.5s infinite alternate;
  box-shadow: 0 0 10px rgba(76, 0, 255, 0.5), 0 0 20px rgba(0, 187, 255, 0.5);
}
</style>
