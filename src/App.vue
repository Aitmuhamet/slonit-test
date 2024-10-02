<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  methods: {
    formatComputerWord(number) {
      const stringNumber = number.toString();
      if (number % 10 === 1 && number !== 11) {
        return `${stringNumber} компьютер`
      } else if (
        number % 10 > 1 && 
        number % 10 < 5 &&
        (number < 5 || 
        number > 20)
      ) {
        return `${stringNumber} компьютера`
      } else {
        return `${stringNumber} компьютеров`
      }
    },
    findCommonDivisors(numbersArray) {
      const minNumb = numbersArray.sort((a, b) => a - b)[0]
      const result = [];

      for (let index = 2; index < minNumb; index++) {
        const divisibleArray = numbersArray.filter(function (item) {
          return item % index === 0;
        })

        if (divisibleArray.length === numbersArray.length) {
          result.push(index);
        }
      }

      return result;
    },
    getPrimesInRange(start, end) {
      const result = [];
      let index = start === 1 ? 2 : start;
      for (; index < end; index++) {
        const number = index;
        let isPrime = true;
        for (let j = 2; j < number; j++) {
          if (number % j === 0) {
            isPrime = false;
            break;
          }
        }
        if (isPrime) result.push(number);
      }
      return result;
    },
    printMultiplicationTable(n) {
      let line = '';
      const cellLength = (n * n).toString().length;


      for (let i = 0; i <= n; i++) {
        for (let k = 0; k < (n.toString().length - i.toString().length); k++) {
          line += ' ';
        }
        line += i.toString() === '0' ? ' ' : i.toString();

        for (let j = 1; j <= n; j++) {
          line += ' ';
          const number = i === 0 ? j : (i * j);
          const numberString = number.toString();

          for (let k = 0; k < (cellLength - numberString.length); k++) {
            line += ' ';
          }

          line += numberString;
        }
        console.log(line);
        line = '';
      }
    }
  },
  watch: {
    computersNumber(newValue) {
      this.formatedWord = this.formatComputerWord(newValue);
    }
  },
  mounted() {
    const computersNumber = +prompt('Задача #1. Укажите количество компьютеров в цифрах', 0)
    const formatedWord = this.formatComputerWord(computersNumber)
    console.group('Задача #1. Существительное с числительным в И.п.')
    console.log('Ответ: ', formatedWord);
    console.groupEnd();

    const numbersArray = []
    let number = +prompt('Задача #2. Общие делители. Добавляем число в массив. Чтобы перейти к следующей задаче, нажмите на "Cancel"', 0);
    while (number > 0) {
      numbersArray.push(number);
      number = +prompt('Задача #2. Общие делители. Добавляем число в массив. Чтобы перейти к следующей задаче, нажмите на "Cancel"', 0);
    }
    const commonDivisors = this.findCommonDivisors(numbersArray)
    console.group('Задача #2. Массив чисел, которые являются общими делителями для всех указанных чисел.')
    console.log('Ответ: ', commonDivisors);
    console.groupEnd();

    const beginningRange = +prompt('Задача #3. Простые числа. Введите минимальное число для диапазона', 0)
    const endingRange = +prompt('Задача #3. Простые числа. Введите максимальное число для диапазона', 0)
    const primesInRange = this.getPrimesInRange(beginningRange, endingRange);
    console.group(`Задача #3. Простые числа в диапазоне от ${beginningRange} до ${endingRange}`)
    console.log('Ответ: ', primesInRange);
    console.groupEnd();

    const sizeMultiplicationTable = +prompt('Укажите размер таблицы умножения', 0);
    console.group('Задача #4. Таблица умножения')
    this.printMultiplicationTable(sizeMultiplicationTable);
    console.groupEnd();

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
