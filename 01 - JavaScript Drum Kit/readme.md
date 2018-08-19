# Js Drum Kit
Day 1  用事件聆聽，監聽鍵盤(keydown)動作，而去播放對應的音樂 

## code 流程

1. **取得鍵盤的Keycode**

>鍵盤上每個按鍵都有個 Keycode，可以再 [keycode.info](http://keycode.info/") ，查到每個按鍵的 keycode.

2. **Html標籤中,新增 data-屬性**


3. **動作流程的判斷**

 

 ### <kbd>data-* 屬性</kbd> 

自訂意義的標籤屬性，可以用Javascript & Css 讀取到並應用

 ```html
    <div data-key="65" class="key">
      <kbd>A</kbd>
      <span class="sound">clap</span>
    </div>
    <audio data-key="65" src="sounds/clap.wav"></audio>
```
在使用 data-* 屬性時，* 字號的地方不能包含大寫字母，也就是屬性名稱不能包含大寫字母，而屬性值則可以是任何的"字串"。

## 使用 JS 取得 data-* 屬性
 ```javascript
  Const key =  document.queryselector('key');
  function (key){
  console.log(key.dataset); // "99"
  console.log(key.keycode); // "99"
  }
```
## CSS 取得或選取 data-*屬性 
也能用在 Css內的偽元素 `::befor` `::after`
```css
div::before{
  content: attr(data-key);
}
```
或是直接用選取器的方式選取

```css
div::before{
  content: attr(data-key);
}

.key kbd[data-key="65"] {
  font-size: 20px;
}
.key span[data-key="65"] {
 font-size: 25px;
}
```
### currentTime 

可以取得當前影音媒體的時間，或是直接設定媒體時間

 ```javascript
      audio.currentTime = 0; //將audio底下的聲音初始秒數
```










