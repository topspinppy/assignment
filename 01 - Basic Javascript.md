# 01 - Basic Javascript

## 1.1

```js
function displayIntroduceMessage(firstName: string, lastName: string): string {
     const firstNameCondition = firstName === 'Shippop' ? 'Best Online Shipping Platform' : firstName
     return `Hello Shippop, My name is {{${firstNameCondition}}} {{${lastName}}}`
}

const messageOne = displayIntroduceMessage('Paranat', 'Klinhom')
console.log(messageOne) // "Hello Shippop, My name is {{Paranat}} {{Klinhom}}"

const messageTwo = displayIntroduceMessage('Shippop', 'Klinhom')
console.log(messageTwo)  // "Hello Shippop, My name is {{Best Online Shipping Platform}} {{Klinhom}}"
```

## 1.2 
```js
const arrayExample = ["1","2","3","4"]
const arrayExampleClone = [...arrayExample]

// example
// [arrayExample === arrayExampleClone]
// false ---> it's pointing to a new memory space
```
## 1.3

First class function คือ การกำหนดให้ function เป็นตัวแปรได้ โดยมันจะถูกมองเป็น Data type แบบหนึ่ง ซึ่งจะต่างกับการ declare function แบบปกติ โดย ถ้า declare function ปกติ จะมี Scope แบบ Global แต่ถ้าเป็นตัวแปร เราจะต้องสร้างก่อนตัวแปรไม่ได้ เราจะสร้างได้แค่หลังตัวแปรเท่านั้น

ตัวอย่าง "การประกาศตัวแปร
```js
const a = function add (x, y) {
     return x + y
}

const b = a(1, 2)
// Result: 3

```