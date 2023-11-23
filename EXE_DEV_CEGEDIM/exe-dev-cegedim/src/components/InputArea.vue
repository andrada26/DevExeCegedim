
<template>
  <div class="userInput">
    <div class="divInputStyle"><input class="inputStyle" type="text" v-model="inputText"
        placeholder="Introduceti numerele aici..." /></div>
    <div class="divButtonStyle"><button class="buttonStyle" @click="createMax">Calculate</button></div>
  </div>
  <div class="container">
    <div class="tableStyle">
      <table v-if="bMatrix.length > 0">
        <thead>
          <tr>
            <th class="tittleStyle">Număr</th>
            <th class="tittleStyle">Prima Cifră</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(row, index) in bMatrix" :key="index">
            <td>{{ row[0] }}</td>
            <td>{{ row[1] }}</td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="maxStyle" v-if="bMaxMatrix.length > 0">
      <p v-if="bMaxMatrix.length > 0">
        <strong>Maximele din clase sunt :</strong> {{ bMaxMatrix }}
        <br>
      </p>
      <p v-if="charResult.length > 0">
        <strong>Modulo :</strong> {{ charResult }}
        <br>
      </p>
    </div>
  </div>
  <div class="matrixStyle">
    <table class="table2Style" v-if="cMatrix.length > 0">
      <tbody>
        <tr class="rowStyle" v-for="(row, rowIndex) in 4" :key="rowIndex">
            <td class="colStyle" v-for="(col, colIndex) in 4" :key="colIndex">{{ cMatrix[rowIndex * 4 + colIndex] }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref } from 'vue';


const inputText = ref('');
const bMatrix = ref([]);
const bMaxMatrix = [];
const cMatrix = ref([]);
const charResult = [];


const createMax = () => {

  const numbers = inputText.value.split(",");
  let smallestInteger = Number.MIN_SAFE_INTEGER;

  for (const number of numbers) {
    const firstDigit = Number(number[0]);
    bMatrix.value.push([Number(number), firstDigit]);
  }


  for (let k = 0; k < 10; k++) {
    smallestInteger = Number.MIN_SAFE_INTEGER;
    let foundclass = 0;

    for (let i = 0; i < bMatrix.value.length; i++) {

      if (bMatrix.value[i][0] > smallestInteger && k == bMatrix.value[i][1]) {
        console.log(`Verificam: ${smallestInteger} cu ${bMatrix.value[i][0]}`);
        smallestInteger = bMatrix.value[i][0];
        foundclass = 1;
      }

    }
    if (foundclass == 1)
      bMaxMatrix.push(smallestInteger);

  }
  toChar(bMaxMatrix);

};
const toChar = (numbers) => {

  for (const number of numbers) {
    let numericValue = Number(number);
    //aducem numărul în intervalul [0, 25]
    numericValue = ((numericValue % 26) + 26) % 26;


    const correspondingLetter = String.fromCharCode("A".charCodeAt(0) + numericValue);

    console.log(correspondingLetter);
    charResult.push(correspondingLetter);

  }
  createCMatrix(charResult);
};

const createCMatrix = (charResult) => {

  for (let i = 0; i < 4; i++) {
    for (let j = 0; j < 4; j++) {
      const randomIndex = Math.floor(Math.random() * charResult.length);
      console.log(`S-a ales indexul random: ${randomIndex} cu valoarea  ${charResult[randomIndex]}`);
      cMatrix.value.push(charResult[randomIndex]);

    }

  }
  return cMatrix;
};
</script>



<style scoped>
h3 {
  margin: 40px 0 0;
}

.divInputStyle {
  height: 100%;
  width: 100%;
}

.userInput {
  margin-bottom: 45px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.inputStyle {
  height: 20px;
  width: 100%;
}

.divButtonStyle {
  display: inline-block;
}

.buttonStyle {
  height: 27px;
}

.container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.tableStyle {
  display: inline-block;
}

.tittleStyle {
  padding-left: 10px;
}

.maxStyle {
  display: inline-block;
  border: solid;
  border-radius: 2px;
  border-color: blue;
  border-width: 2px;
}

.matrixStyle {
  display: flex;
  justify-content: center;
  align-items: center;
}

.table2Style{
  width: 100%;
}
.rowStyle{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
}

.colStyle{
  margin-top: 2rem;
  margin-bottom: 2rem;
}
</style>
