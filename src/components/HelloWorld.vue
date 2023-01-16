<template>
  <div>
    <h1>PV-Förderung</h1>
    <p>
      PV - FördererungenEAG-Investitionszuschuss Photovoltaik und Stromspeicher
      im Jahr 2023Mit dem Erneuerbaren-Ausbau-Gesetz (EAG) wurden die
      rechtlichen Rahmenbedingungen für den Netzanschluss von erneuerbaren
      Energieanlagen vereinfacht. Dies umfasst auch finanzielleErleichterungen
      in Form eines pauschalierten Netzzutrittsentgelts. Mit einem der
      EAG-Investitionszuschüsse werden die Neuerrichtung und Erweiterung von
      Photovoltaikanlagen und die damit verbundene Neuerrichtung von
      Stromspeichern gefördert. Für die Erweiterung einer Photovoltaikanlage ist
      keine Mindestgröße vorgesehen.
    </p>
    <h1>Bisherige Ansuchen (Max. Fördersumme: {{ maxFunding }}€)</h1>
    <div>
      <table class="table">
        <thead>
          <th>Name:</th>
          <th>PLZ:</th>
          <th>Zählpunkt:</th>
          <th>kwPeak:</th>
          <th>Bewilligt:</th>
        </thead>
        <tbody>
          <tr v-for="(item, index) in items" :key="item.zaehlpunkt">
            <td>{{ item.name }}</td>
            <td>{{ item.plz }}</td>

          <td>
            <input
              ref="zaehlpunktInput"
              type="text"
              v-model="item.zaehlpunkt"
              @blur="updatezaehlpunkt(item)"
            />
            <button @click="editzaehlpunkt(item)">Edit</button>
          </td>

           <td>
            <input
              ref="kwPeakInput"
              type="text"
              v-model="item.kwPeak"
              @blur="updateKwPeak(item)"
            />
            <button @click="editKwPeak(item)">Edit</button>
          </td>

            <td>
              <td>
                <input 
                type="checkbox" 
                v-model="item.bewilligt" 
                @change="handleCheckboxChange(item)" />
              </td>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import items from './data.js';

export default {
  name: 'HelloWorld',
  data: function() {
    return {
      maxFunding: 10000000,
      isChecked: false,
    }
  },
  props: ['maxFunding'],
  props: {
    items: { type: Array, required: true },
  },
methods: {
  editzaehlpunkt(item) {
      // set the kwPeak value to an empty string to allow editing
      item.zaehlpunkt = '';
    },
    updatezaehlpunkt(item) {
      console.log(item.zaehlpunkt);
      // You can use the value of item.kwPeak here to update the data in your server or in local storage
    },
  editKwPeak(item) {
      // set the kwPeak value to an empty string to allow editing
      item.kwPeak = '';
    },
    updateKwPeak(item) {
    var decimal = /^[-+]?[0-9]+\.[0-9]+$/;
    if(!decimal.test(item.kwPeak))
    {
        alert("kwPeak should be a decimal number")
        item.kwPeak = '';
        return
    }
    console.log(item.kwPeak);
    // You can use the value of item.kwPeak here to update the data in your server or in local storage
},
    updateBewilligt(index) {
      this.$emit('update-application', index);
    },
  handleCheckboxChange(item) {
    console.log(`The checkbox value for ${item.name} is: ${item.bewilligt}`)
  },
  },
};
</script>
<style>
table {
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  border: 1px solid black;
  padding: 8px;
  text-align: left;
}

th {
  background-color: lightgrey;
  font-weight: bold;
}

tr:nth-child(even) {
  background-color: #f2f2f2;
}
</style>
