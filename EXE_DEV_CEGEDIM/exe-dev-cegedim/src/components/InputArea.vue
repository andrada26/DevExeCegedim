
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
  <div class="matrixStyle" v-if="bMaxMatrix.length > 0">
    <table class="table2Style" v-if="cMatrix.length > 0 && calculate.value != 2">
      <tbody>
        <tr class="rowStyle" v-for="(row, rowIndex) in cMatrix" :key="rowIndex">
          <td class="colStyle" v-for="(col, colIndex) in cMatrix" :key="colIndex"
            @click="handlecClick(rowIndex, colIndex)">{{ cDisplay[rowIndex][colIndex] }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref } from 'vue';


const inputText = ref('');
const bMatrix = ref([]);
const bMaxMatrix = ref([]);
const charResult = ref([]);
const calculate = ref(0);
const cMatrix = ref(Array.from({ length: 4 }, () => Array(4).fill("")));
const cDisplay = ref(Array.from({ length: 4 }, () => Array(4).fill("?")));
const cClicked = ref(Array.from({ length: 4 }, () => Array(4).fill("0")));

const createMax = () => {

  calculate.value += 1;

  if (calculate.value === 2) {
    bMatrix.value = [];
    bMaxMatrix.value = [];
    charResult.value = [];
    calculate.value = 0;
  }

  const numbers = inputText.value.split(",");
  let smallestInteger = ref(Number.MIN_SAFE_INTEGER);
  let index = ref(0);

  for (const number of numbers) {
    const firstDigit = Number(number[0]);
    bMatrix.value.push([Number(number), firstDigit]);
  }


  for (let k = 0; k < 10; k++) {
    smallestInteger = ref(Number.MIN_SAFE_INTEGER);
    let foundclass = 0;


    for (let i = 0; i < bMatrix.value.length; i++) {

      if (bMatrix.value[i][0] > smallestInteger.value && k == bMatrix.value[i][1]) {
        console.log(`Verificam: ${smallestInteger.value} cu ${bMatrix.value[i][0]}`);
        smallestInteger.value = bMatrix.value[i][0];
        foundclass = 1;

      }

    }
    if (foundclass == 1) {
      console.log(`Max = bMaxMatrix.value[${index.value}] = ${bMaxMatrix.value[index.value]} smallestInteger: ${smallestInteger.value} `);
      bMaxMatrix.value[index.value] = (smallestInteger.value);
      index.value += 1;
    }
  }
  toChar(bMaxMatrix);

};
const toChar = (numbers) => {

  let index = 0;

  for (let i = 0; i < numbers.value.length; i++) {
    let numericValue = numbers.value[i];
    //aducem numărul în intervalul [0, 25]
    numericValue = ((numericValue % 26) + 26) % 26;


    const correspondingLetter = String.fromCharCode("A".charCodeAt(0) + numericValue);

    console.log(correspondingLetter);
    charResult.value[index] = (correspondingLetter);
    index++;

  }
  createCMatrix(charResult);
};

const createCMatrix = (charResult) => {

  //const clickedTd = ref([]);
  for (let i = 0; i < 4; i++) {
    for (let j = 0; j < 4; j++) {
      const randomIndex = Math.floor(Math.random() * charResult.value.length);
      //console.log(`S-a ales indexul random: ${randomIndex} cu valoarea  ${charResult.value[randomIndex]}`);
      cMatrix.value[i][j] = charResult.value[randomIndex];

    }
  }

  for (let i = 0; i < 4; i++) {
    console.log(`linia ${i}:`);
    for (let j = 0; j < 4; j++) {
      console.log(`${cMatrix.value[i][j]}`);
    }

  }
  return cMatrix;
};
const handlecClick = (rowIndex, colIndex) => {

  console.log(`Ati apasat pe randul ${rowIndex} si coloana ${colIndex}`)

  if (cClicked.value[rowIndex][colIndex] == 0) {
    // not clicked => display "?"
    console.log(`nu era apasat`)
    cDisplay.value[rowIndex][colIndex] = cMatrix.value[rowIndex][colIndex];
    cClicked.value[rowIndex][colIndex] = 1;
  } else {
    //  clicked => display char
    cDisplay.value[rowIndex][colIndex] = "?";
    cClicked.value[rowIndex][colIndex] = 0;
  }
  console.log(`cDisplay: ${cDisplay.value[rowIndex][colIndex]} si cClicked ${cClicked.value[rowIndex][colIndex]}`)

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
  margin-bottom: 4rem;
}

.tableStyle {
  display: inline-block;
  margin-right: 2rem;
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

.table2Style {
  width: 60%;
}

.rowStyle {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
}

.colStyle {
  height: 4.5rem;
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: url("E:\EXE_DEV_CEGEDIM\other\bgd.png"); 
  background-size: contain; 
  background-position: center; 
  background-repeat: no-repeat;
}
</style>
