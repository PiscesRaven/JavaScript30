# Day 5 Flex Panel Gallery

## code 流程

1. **對每個 `panel`增加事件聆聽**

2. **當點擊的時候做動畫**


### CSS語法

CSS就用到了 `display: flex`、`flex`、`flex-direction`、`justify-content` 等等樣式

Class的部分則是:`.open`、`open-active`

主要還是靠 這兩個CSS與JS達到動畫的效果


### code處理

```javascript
   function Anime() {
      this.classList.toggle('open');
      this.classList.toggle('open-active');
    }
    document.querySelectorAll('.panel').forEach(panel => { panel.addEventListener('click', Anime); });
    
```

demo的範例

```javascript
panel.addEventListener('click', Fn);
panel.addEventListener('transitionend', Fn);
```

個人寫法跟 Demo範例有些不同，範例中的 `addEventListener()`
使用到了 `transitionend` ，當 click 設定的動畫結束時，會執行function ，但是做法有個視覺上小Bug，就是當如果是連點的時候會，呈現出跟原本預設的動畫相反的情況(圖片縮小後，文字才會出現)。<br>
會造成這個原因是因為 `transitionend` 還沒觸發，又因為 `click` 的再次觸發，所以效果就會變成相反的情況。
#### 解決方法
把 panel > * `transition`增加一個`delay` 值，運用延遲讓圖片先伸縮再來讓文字移動。

```CSS
  .panel>* {
      transition: transform 0.5s 0.8s;
    }
```





