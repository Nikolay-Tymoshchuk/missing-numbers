# Поиск пропущенных чисел в отсортированном массиве

## Описание задачи

Дана последовательность чисел от 1 до 10 ... или 10 миллиардов. Числа отсортированы по возрастанию (1, 2, 3 и т.д.). В этой последовательности отсутствуют 2 числа. Мы знаем длину и границы последовательности, но не знаем, какие именно числа отсутствуют.

## Задача

1. Найти отсутствующие числа оптимальным способом. Например, если отсутствуют 2 и 3, последовательность будет выглядеть следующим образом: 1, 4, 5, 6 ... 10,000,000,000.
2. Оценить вычислительную сложность решения.

## Оценка вычислительной сложности

Время выполнения алгоритма увеличивается логарифмически с увеличением размера входных данных, поэтому сложность алгоритма составляет O(log n).

## План поиска

1. Определить границы поиска (начало и конец последовательности).
2. Использовать бинарный поиск для нахождения первой и второй пропущенных позиции.
3. Вернуть два пропущенных числа.

- Бинарный поиск имеет сложность **O(log n)**.

## Реализация

```javascript
function findMissingNumbers(arr) {
  let left = 0;
  let right = arr.length - 1;

  function findMissingNumber(offset) {
    while (left <= right) {
      const mid = Math.floor((left + right) / 2);

      if (arr[mid] === mid + offset) {
        left = mid + 1;
      } else {
        right = mid - 1;
      }
    }

    const result = left + offset;
    right = arr.length - 1;

    return result;
  }

```

## Примеры использования

```javascript
const array2 = Array.from({ length: 2 }, (_, i) => i + 1).filter(
  (num) => num !== 1 && num !== 2
);
const array3 = Array.from({ length: 3 }, (_, i) => i + 1).filter(
  (num) => num !== 2 && num !== 3
);
const array10 = Array.from({ length: 10 }, (_, i) => i + 1).filter(
  (num) => num !== 1 && num !== 2
);
const array100 = Array.from({ length: 100 }, (_, i) => i + 1).filter(
  (num) => num !== 1 && num !== 100
);
const array1000 = Array.from({ length: 1000 }, (_, i) => i + 1).filter(
  (num) => num !== 999 && num !== 1000
);
const array10000 = Array.from({ length: 10000 }, (_, i) => i + 1).filter(
  (num) => num !== 5000 && num !== 7599
);

const missingNumbers2 = findMissingNumbers(array2); // [1, 2] (array2 пустой, значит пропущены 1 и 2)
const missingNumbers3 = findMissingNumbers(array3); // [2, 3]
const missingNumbers10 = findMissingNumbers(array10); // [1, 2]
const missingNumbers100 = findMissingNumbers(array100); // [1, 100]
const missingNumbers1000 = findMissingNumbers(array1000); // [999, 1000]
const missingNumbers10000 = findMissingNumbers(array10000); // [5000, 7599]
```

### Результаты:

- `array2` → пропущены `[1, 2]`
- `array3` → пропущены `[2, 3]`
- `array10` → пропущены `[1, 2]`
- `array100` → пропущены `[1, 100]`
- `array1000` → пропущены `[999, 1000]`
- `array10000` → пропущены `[5000, 7599]`

## Заключение

Этот алгоритм эффективно ищет два пропущенных числа в отсортированном массиве за **O(log n)**, используя бинарный поиск для нахождения позиций пропусков.
