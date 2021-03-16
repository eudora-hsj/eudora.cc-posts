---
title: '[JS] Array 陣列基本操作'
tags: [JavaScript, Array]
category: JavaScript
#   - - (所有文章)
#   - - 工程師－攻城路
#     - JavaScript
permalink: posts/26137
date: 2021-01-13 08:00:42
---

示例 JavaScript 中操作 Array 的幾種方法。

<!--more--> 

## Array
- 基本寫法
    ```javascript
    var arr = [
        "A",
        "B",
        "C"
    ];
    ```
  等同於
    ```javascript
    var arr = new Array("A", "B", "C");
    ```
    - 最後一個值後面不要加逗號
    - 換行不換行都沒差
    
- `[ ]` 取陣列值第幾個  
  arr[0] 第一個陣列值  
  arr[-1] 最後一個陣列值
  
  
- `arr.length` 取陣列長度
- `arr.sort()` 陣列內重排序

---


## 陣列操作的幾種方法


```javascript
let friends = ['Amy', 'Berry', 'Claire']
```

## ◎`for...in` ：迭代 屬性（key） 
```javascript
for (let index in friends){
    console.log(index)             // 0, 1, 2
    console.log(friends[index])    // Amy, Betty, Claire
}
```

 ## ◎`for...of`：迭代陣列值
 
```javascript
for (let friend of friends){
    console.log(friend)         // Amy, Betty, Claire
}
```
- 延伸：如果想要迭代物件的話：使用`Object.keys()`：
  
    ```javascript
    let obj = {
        key1: 'value1',
        key2: 'value2',
        key3: 'value3'
    }
    ```
    ```javascript
    for (let key of Object.keys(obj)){
        console.log(key + ": " + obj[key])
        // key1: value1, key2: value2, key3: value3
    }
    ```



## ◎`forEach()`：歷遍每一個元素執行  

```javascript
friends.forEach(friend => 
    console.log(friend)    // / Amy, Betty, Claire
)
```
```javascript
friends.forEach((friend, index) => {
        console.log(`${index}-${friend}`)   
        // / 0-Amy, 1-Betty, 2-Claire
    } 
)
```

---

```javascript
let numbers = [1, 2, 3]
```

### ◎`map()`：將每一次的結果集合為一個新陣列回傳

```javascript
let mapNumbers = numbers.map(number =>
    number * 2
)
console.log(mapNumbers)  // 2, 4 , 6
```

 

### ◎`reduce()` 操作參數包含前次結果(可用於累加)

```javascript
let reduceNumbers = numbers.reduce((number, sum) =>
    number + sum
    ,0
)
console.log(reduceNumbers)  // 6  (1+2+3)
```

### ◎`filter()`：回傳所有符合條件的元素

```javascript
let filterNumbers = nums.filter( num => 
        num > 10    
)
console.log(filterNumbers)  // [11, 13] 
```

### ◎`find()`：回傳第一個符合條件的元素

```javascript
let findNumbers = nums.find( num => 
    num > 10    
)
console.log(findNumbers)  // 11 
```

---

```javascript
let nums = [1, 3 , 5, 7,  9 , 11 , 13]
```

### ◎`some()` ：只要有１個以上符合條件，就為 true

```javascript
let someNumbers = nums.some( num => 
    num > 10    
)
console.log(someNumbers)  // true 
```

### ◎`every()` ：每一個都符合時才會回傳 true

```javascript
let everyNumbers = nums.every( num => 
    num > 10    
)
console.log(everyNumbers)  // false 
```

---

參考文件：
- [Array｜MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [JS-for...in與for...of的差別](https://kanboo.github.io/2018/01/30/JS-for-of-forin/)

---

本文同步發表在[第 12 屆 iT 邦幫忙鐵人賽 《For 前端小幼苗的圖解筆記》](https://ithelp.ithome.com.tw/articles/10246679)


