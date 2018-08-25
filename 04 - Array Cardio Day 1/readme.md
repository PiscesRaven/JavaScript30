# Day 04 Array Cardio v1

Day 3 Array 的基本應用 `filter()`、`map()`、`sort()`、`reduce()`的基本用法

其中有兩個`filter`、`map`是 ES5 定義的迭代方法，這些迭代方法都有一個特點，就是對 `Array`的每一項都運行給定函數，根據使用的迭代方法的不同，有不同的返回結果。

## [Array知識補充 JavaScript 陣列處理方法 [filter(), find(), forEach(), map(), every(), some(), reduce()]](https://wcc723.github.io/javascript/2017/06/29/es6-native-array/)


## 要練習的題目為：
1. 篩選出於1500~1599年間出生的inventor(year in 1500-1599)
2. 將inventors內的first與last組合成一個陣列
3. 依據生日由大至小排序所有的inventor
4. 加總所有inventor的在世時間
5. 依據年齡由大至小排序所有的inventor
6. 列出wiki中巴黎所有包含'de'的路名(在wiki中透過querySelectorAll來選取資料作篩選)
7. 依據lastName排序所有people的資料
8. 分別計算data內每個種類的數量


### 1.filter()

題目：篩選出於1500~1599年間出生的inventor(year in 1500-1599)<br>
解答：透過fifter()對來源做篩選，會將結果為true的資料組成陣列回傳

[filter()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter#Syntax)

```javascript
let filters = inventors.filter(inv => inv.year >= 1500 && inv.year < 1600);
```

### 2.map()

題目：將inventors內的first與last組合成一個陣列<br>
解答：透過map來將firstName/lastNam組合變成新陣列

[map()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map#Syntax)

```javascript
let map = inventors.map(inv => inv.first + ' ' + inv.last);
```

### 3.sort()
題目：依據生日由大至小排序所有的inventor
解答：透過sort()來做排序

[sort()](https://msdn.microsoft.com/zh-tw/library/4b4fbfhk(v=vs.94).aspx)

排序方式:方法用於對陣列的內容進行排序，並返回到陣列中。默認排序順序是根據字串的Unicode去排序。



### 4. reduce()

題目：加總所有inventor的在世時間
解答：有多種解法，可用 `reduce()`、`for迴圈`、`forEach`

[reduce()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce#%E8%AF%AD%E6%B3%95)

`forEach解法`

```javascript
let reduce = 0;
    inventors.forEach(inv => {
      reduce += (inv.passed - inv.year);
    });
    console.log(reduce);
// 861
```

如果利用 `reduce()` 搭配箭頭函式如下：

```javascript
let reduceArrow = inventors.reduce((reduce, inv) =>
      reduce += (inv.passed - inv.year)
      , 0);

    console.log(reduceArrow);
// 861
```
`reduce()` 中有4個可以用 callback參數:
1. 初始值
2. 陣列中正在處理的元素
3. 陣列中正在處理的元素的索引值
4. 使用reduce的陣列 及一個預設值(會再第一次執行時賦予第一個參數設定的值。


### 6. map() + filter() + includes() 應用

題目：列出 wiki 中巴黎所有包含'de'的路名 <br>
解答：先用 `querySelectorAll()` 來選取物件，但是 `querySelectorAll()` 所轉出來的 `__proto__` 是`NodeList`，要先用 `Array.from`把NodeList轉換成Array ，再用map+filter+includes來做文字的篩選，若存在’de’就回傳true加入陣列。

```javascript
     const category = document.querySelector('.mw-category');
     const links = Array.from(category.querySelectorAll('a'));
     const de = links
                 .map(link => link.textContent)
                 .filter(streetName => streetName.includes('de'));
```

### 7. sort() & split()
題目：依據lastName排序所有people的資料<br> 
解答：範例中 people 這個Array['Beck, Glenn’]這樣的格式，因為要取得lastName就必須要使用split()來切開Array，再用比較的方式做排序對比 。


```javascript
    let sortLastName = people.sort(function (a, b) {
      let sortA = a.split(", ");
      let sortB = b.split(", ");
      return sortA[1] > sortB[1] ? 1 : -1;
    });
```

### 8. reduce() 出種類數量

題目：分別計算data內每個種類的數量<br>\
解達: 先用空物件，再用reduce 判斷是要增加物件內容還是對物件數量總數 +1


```javascript
 const data = ['car', 'car', 'truck', 'truck', 'bike', 'walk', 'car', 'van', 'bike', 'walk', 'car', 'van', 'car',
      'truck'
    ];
  let carKind = {};
    data.reduce(function (carkind, obj) {
      if (!carKind[obj]) {
        carKind[obj] = 1;
      } else {
        carKind[obj]++;
      }
    }
    );
```

    