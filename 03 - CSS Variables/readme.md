# CSS Variables
Day 3 用JS與CSS搭配製作一個即時的濾淨效果， 特效為調整內距、模糊、邊框色。

1. **CSS 變數**

`root` Css3才有的新功能，設定的值可以在js中讀取到並應用。
```css
:root{
    --base: #ffc600;
    --spacing: 10px;
    --blur: 10pxㄤ
    }
```

2. **addEventLinstener**

利用addEventLinstener來綁HTML的控制桿，
並更新值到CSS變數中來達到即時調整的效果


## code流程 

### CSS 

1. :root
2. 將 `root`的變數應用在對應的 `<img>`
3. 處理標題的css值

### Js 

1. js 取得css的更新值
2. 取得 `input` 
3. 對 `input` 增加監聽事件，可以偵測值的變動，而更新css的值
4. 對 `滑鼠` 增加事件聆聽
5. 取得變數的後輟
6. 取得css變數名稱（blur、spacing、color）
7. 取得css變數值
8. 給予對應的新css變數

## 知識補充

### NodeList 與 Array的差異

NodeList 是由 `querySelectorAll` 是個看起來很像陣列，但實際上不是陣列，這個部分從瀏覽器的 console 可以看到 `proto` 會顯示 `NodeList`。
能使用的 `prototype`，只有 `forEach()`、`item()`、`keys()`，Array 的 `prototype`則可以使用 `map()`、`pop()`、`filter()`..等。

### dataset 

`dataset`用來取得 `html` 標籤內的 `data-* 屬性` 名稱，功用等同於 `getAttribute`

````javascript
<div id="test" data-no="123"></div>
document.querySelector('#test').dataset.no // 輸出123
document.querySelector('#test ').getAttribute('data-no'); // 輸出123
````
### style.setProperty()

可以給css賦予一個新的css的值，等同於style.cssPropertyName

style.setProperty(propertyName, value, priority);

- `propertyName` 要被更換的css屬性。
- `value` 被設定的新值，在沒有指定的情況下可以當作空字串。
P.S value 不能用 `!important`。
- `priority` 用來設定css的優先級，可以帶入 `!important`、`null`或是空字串

````css
style.setProperty('padding', '15px');
/* 等同於 */
style.padding = '15px';
````

### 參數值的處理

這次的練習中，input的標籤內，可調整的因一個有`px`另一個則是色碼調整，所以運用dataset來判斷input中的 `ata-sizing: px`

````html
    <input id="blur" type="range" name="blur" min="0" max="25" value="10" data-sizing="px">
    <input id="base" type="color" name="base" value="#ffc600">
````
透過 dataset.sizing 來取得屬性值。

````javascript
const suffix = this.dataset.sizing || ''; 
````

