
<template>
  <div class="userinput">
    <div class="divInputStyle"><input class="inputStyle" type="text" v-model="inputText"
        placeholder="Introduceti numerele aici..." /></div>
    <div class="divButtonStyle"><button class="buttonStyle" @click="handleButtonClick">Calculate</button></div>
  </div>
  <table v-if="resultMatrix.length > 0">
    <thead>
      <tr>
        <th class="tittleStyle">Număr</th>
        <th class="tittleStyle">Prima Cifră</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(row, index) in resultMatrix" :key="index">
        <td>{{ row[0] }}</td>
        <td>{{ row[1] }}</td>
      </tr>
    </tbody>
  </table>
  <p v-if="resultMaxMatrix.length > 0">
    <strong>Maximele din clase sunt :</strong> {{ resultMaxMatrix }}
    <br>
  </p>
</template>

<script setup>
import { ref } from 'vue';


const inputText = ref('');
const resultMatrix = ref([]);
const resultMaxMatrix = ref([]);

const handleButtonClick = () => {
  resultMatrix.value = []; // Remove last values  
  resultMaxMatrix.value = [];

  const numbers = inputText.value.split(",");
  let smallestInteger = Number.MIN_SAFE_INTEGER;

  for (const number of numbers) {
    const firstDigit = Number(number[0]);
    resultMatrix.value.push([Number(number), firstDigit]);
  }


  for (let k = 0; k < 10; k++) {
    smallestInteger = Number.MIN_SAFE_INTEGER;
    let foundclass = 0;

    for (let i = 0; i < resultMatrix.value.length; i++) {

      if (resultMatrix.value[i][0] > smallestInteger && k == resultMatrix.value[i][1]) {
        console.log(`Verificam: ${smallestInteger} cu ${resultMatrix.value[i][0]}`);
        smallestInteger = resultMatrix.value[i][0];
        foundclass = 1;
      }

    }
    if(foundclass == 1)
    resultMaxMatrix.value.push(smallestInteger);

  }


};
</script>



<style scoped>
h3 {
  margin: 40px 0 0;
}

.divInputStyle {
  display: inline-block;
}

.inputStyle {
  height: 20px;
  width: 600px;
}

.divButtonStyle {
  display: inline-block;
}

.buttonStyle {
  height: 27px;
}

.tittleStyle {
  padding-left: 10px;
}
</style>
