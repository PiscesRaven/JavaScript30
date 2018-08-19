# Js and Css Clock

Day 2 用JS 與 CSS 寫出一個指針時鐘。

1. **取得時間**

`const nowTime = new Date();`

2. **指針角度的CSS對應**

時針會轉動，所以必須要對應 `new Date()`，再將秒、分、時的角度計算出來。
在投過變更 `element.style.tranform` ，來產生位移效果。

3. **計時器**

利用 `setInterval(setTime, 1000);` 每秒取得當前時間。


## Css語法備註 

#### transform-oragin
可以設定物件的中心點，原始設定點在物件的中心X與Y軸的50%的位置
範例中 設定為 100% 使可以再時鐘的中心點上選轉。
這個css等同於



#### transform:rotate()
`transform:rotate()` 旋轉物件，數值後方要加上角度deg，可超過360度，正值為順時針轉，負值為逆時針旋轉，為了讓秒、分、時針，初始位置在一般時鐘的整點位置，所以Css會設定`transform:rotate(90 deg)` 。

#### transition-timing-function: cubic-bezier()

設定動畫轉場所依據的貝茲曲線，可以透過chrome的開發者工具來進行可視化調整。

> [MDN-transform](https://developer.mozilla.org/en-US/docs/Web/CSS/transform?v=control)


## Js語法應用

### 立即函式

 ```javascript
    (function(){
    //code
    })()
```
立即函式是Javascript中一種可以立即執行的函式，其本質其實是個函式表示式。下面程式碼代表著一個簡單的立即函式。
> [Day20　立即呼叫的函式表示式(IIFE)](https://ithelp.ithome.com.tw/articles/10193313)

### 指針角度的計算與設定 

初始設定 `transform:rotate(90 deg)`，是為了讓時針的位置在時鐘的整點位置，方便在顯示的時候是正確的時間位置，但角度的算法還是以`360°`下去計算每個分秒時的移動角度，最後還要加上`90°`，因為我們起始角度就是`90°`。
這個部分就是個數學題，計算方式 :
<pre>
秒數為例
((seconds / 60) * 360) + 90;
((360/60) * seconds) + 90;

</pre>

 ```javascript
    const seconds = nowTime.getSeconds();
    const secondsDegress = ((seconds / 60) * 360) + 90;
    const mins = nowTime.getMinutes();
    const minsDegress = ((mins / 60) * 360) + ((6/60)*seconds) + 90;
    const hours = nowTime.getHours();
    const hourDegress = ((hours / 12) * 360) + ((30/60)*mins) + 90;
```
為了讓指針移動的更真實，所以在 `((mins / 60) * 360)`+`((6/60)*seconds)`,前面的 `((mins / 60) * 360)` 是計算每分鐘的指針角度，`((6/60)*seconds)`則是計算每秒指移動後會增加時針的角度。
分針每分鐘移動的角度為 `6°`/ 60秒*當前的秒數，這樣的作法，讓分針增加秒針移動時，分針也會往下一個分鐘推進 。<br>

時針的計算方式，`((hours / 12) * 360) + ((30/60)*mins)`。<br>>
`((30/60)*mins)`是計算每小時，時針推進會是5小格，所以是 `30°`的推進，在除60分鐘*當前的分鐘，這樣的加總就會在分針越往整點移動時，時針也會跟著推進。


### 指針角度整點的彈跳問題 
 這個時鐘卻存在一個小瑕疵，當指針旋轉一圈之後回到初始位置開始第二圈旋轉，角度值的變化時 `444°→90°→96°`....這個過程中，指針會先逆時針，然後再從90° 開始，會這樣是因為css中有寫`transition: all 0.5s;`，所以每次都會有 0.05s的延遲，解決方法其中一種直接把CSS拿掉，另一種就是判斷當轉一圈時，把`transition` 設定成 0 ，這樣就不會有指針逆時針的效果了。


```javascript
    if (secondsDegress === 90)
        secondHand.style.transition = 'all 0s';
    else secondHand.style.transition = 'all 0.05s';

```









