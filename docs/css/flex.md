# å¼¹æ§å¸å±

ð Flex æ¯ Flexible Box çç¼©åï¼æä¸º"å¼¹æ§å¸å±"ï¼å¯ä»¥è½»æ¾çæ§å¶åç´ æåãå¯¹é½åé¡ºåºçæ§å¶ã

ç°å¨çç»ç«¯ç±»åéå¸¸å¤ï¼ä½¿ç¨å¼¹æ§çæ¨¡åå¯ä»¥è®©åç´ å¨ä¸åå°ºå¯¸ç»ç«¯æ§å¶å°ºå¯¸ã

## å¼å®¹æ§

ä¸é¢æ¯FLEXç³»ç»å¼å®¹æ§æ°æ®ï¼å¨ [https://caniuse.com/ (opens new window)](https://caniuse.com/)ç½ç«æ¥çï¼ç»å¤§å¤æ°è®¾å¤å°¤å¶æ¯**ç§»å¨ç«¯**é½å¾å¥½çæ¯æFLEXï¼æä»¥å¯ä»¥æ¾å¿ä½¿ç¨ã

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/1.png)

## å¼¹æ§çå­

### å£°æå®ä¹

ð å®¹å¨çå­éé¢åå«çå®¹å¨åç´ ï¼ä½¿ç¨ `display:flex` æ `display:inline-flex` å£°æä¸ºå¼¹æ§çå­ã

**å£°æåçº§å¼¹æ§çå­**

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/2.png)

```html
<style>
  * {
    padding: 0;
    margin: 0;
  }
  article {
    height: 150px;
    margin-left: 100px;
    margin-top: 100px;
    outline: solid 5px silver;
    display: flex;
    padding: 20px;
  }
  article div {
    outline: solid 5px blueviolet;
    text-align: center;
    font-size: 28px;
    line-height: 5em;
    width: 300px;
  }
</style>

<article>
  <div>1</div>
	<div>2</div>
	<div>3</div>
</article>
```

**å£°æåèçº§å¼¹æ§çå­**

```css
article {
    display: inline-flex
}
```

### flex-direction

ð ç¨äºæ§å¶çå­åç´ æåçæ¹åã

| å¼             | æè¿°                           |
| :------------- | :----------------------------- |
| row            | ä»å·¦å°å³æ°´å¹³æååç´ ï¼é»è®¤å¼ï¼ |
| row-reverse    | ä»å³åå·¦æååç´                |
| column         | ä»ä¸å°ä¸åç´æååç´            |
| column-reverse | ä»ä¸å°ä¸åç´æååç´            |

**row-reverse**

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/3.png)

```html
<style>
    * {
        padding: 0;
        margin: 0;
    }
    body {
        margin: 100px;
        font-size: 14px;
        color: #555;
    }
    article {
        width: 500px;
        border: solid 5px silver;
        display: flex;
        box-sizing: border-box;
        padding: 10px;
        flex-direction: row-reverse;
    }
    article * {
        border: solid 5px blueviolet;
        padding: 10px;
        margin: 10px;
    }
</style>

<article>
    <h4>A</h4>
    <span>B</span>
    <p>C</p>
</article>
```

**column-reverse**

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/4.png)

```css
article {
    flex-direction: column-reverse;
}
```

### flex-wrap

ð flex-wrap å±æ§è§å®flexå®¹å¨æ¯åè¡æèå¤è¡ï¼åæ¶æ¨ªè½´çæ¹åå³å®äºæ°è¡å å çæ¹åã

| éé¡¹         | è¯´æ                                             |
| :----------- | :----------------------------------------------- |
| nowrap       | åç´ ä¸æè¡æä¸æåï¼é»è®¤å¼ï¼                     |
| wrap         | å®¹å¨åç´ å¨å¿è¦çæ¶åæè¡ææåã                 |
| wrap-reverse | å®¹å¨åç´ å¨å¿è¦çæ¶åæè¡ææåï¼ä½æ¯ä»¥ç¸åçé¡ºåº |

**è¡åç´ æ¢è¡**

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/5.png)

```html
<style>
	* {
    padding: 0;
    margin: 0;
    outline: solid 1px silver;
    padding: 10px;
    margin: 10px;
  }
  head {
    display: block;
  }
  body {
    font-size: 14px;
    color: #555;
  }
  article {
    width: 500px;
    border: solid 5px silver;
    box-sizing: border-box;
    padding: 10px;
    display: flex;
    flex-direction: row;
    /* æå®å¼¹æ§çå­è¶åºæ¢è¡ */
    flex-wrap: wrap;
  }
  article div {
    border: solid 5px blueviolet;
    padding: 30px 80px;
    margin: 10px;
    text-align: center;
    font-size: 28px;
  }
</style>

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

**æ°´å¹³æåååæ¢è¡**

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/6.png)

```css
flex-direction: row;
flex-wrap: wrap-reverse;
```

**åç´åç´ æ¢è¡**

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/7.png)

```css
flex-direction: column;
flex-wrap: wrap;
```

**åç´åç´ ååæ¢è¡**

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/8.png)

```text
flex-direction: column;
flex-wrap: wrap-reverse;
```

### flex-flow

ð `flex-flow` æ¯ `flex-direction` ä¸ `flex-wrap` çç»åç®åæ¨¡å¼ã

ä¸é¢æ¯ä»å³åå·¦æåï¼æ¢è¡åä¸æåè¡ã

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/9.png)

```css
flex-flow: row-reverse wrap-reverse;
```

### è½´è¯´æ

**æ°´å¹³æå**

ä¸é¢æ¯ä½¿ç¨ `flex-flow: row wrap` çä¸»è½´ä¸äº¤åè½´è¯´æã

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/10.png)

ä¸é¢æ¯ä½¿ç¨ `flex-flow: row-reverse wrap-reverse` çä¸»è½´ä¸äº¤åè½´è¯´æã

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/11.png)

**åç´æå**

ä¸é¢æ¯ä½¿ç¨ `flex-flow: column wrap` çä¸»è½´ä¸äº¤åè½´è¯´æã

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/12.png)

### justify-content

ð ç¨äºæ§å¶åç´ å¨ä¸»è½´ä¸çæåæ¹å¼ï¼åæ¬¡å¼ºè°æ¯**ä¸»è½´**çæåæ¹å¼ã

| éé¡¹          | è¯´æ                                                         |
| :------------ | :----------------------------------------------------------- |
| flex-start    | åç´ ç´§é ä¸»è½´èµ·ç¹                                             |
| flex-end      | åç´ ç´§é ä¸»è½´ç»ç¹                                             |
| center        | åç´ ä»å¼¹æ§å®¹å¨ä¸­å¿å¼å§                                       |
| space-between | ç¬¬ä¸ä¸ªåç´ é èµ·ç¹ï¼æåä¸ä¸ªåç´ é ç»ç¹ï¼ä½ä¸åç´ å¹³ååéç©ºé´   |
| space-around  | æ¯ä¸ªåç´ ä¸¤ä¾§çé´éç¸ç­ãæä»¥ï¼åç´ ä¹é´çé´éæ¯åç´ ä¸å®¹å¨çè¾¹è·çé´éå¤§ä¸å |
| space-evenly  | åç´ é´è·ç¦»å¹³ååé                                           |

æ°´å¹³æååç´ ï¼å¹¶ä½¿ç¨ `justify-content: flex-end` å¯¹é½å°ä¸»è½´ç»ç¹

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/13.png)

```html
<style>
    * {
        padding: 0;
        margin: 0;
        padding: 10px;
        margin: 10px;
    }
    body {
        font-size: 14px;
        color: #555;
    }
    article {
        border: solid 5px silver;
        box-sizing: border-box;
        display: flex;
        flex-flow: row wrap;
        /* ç´§é ä¸»è½´å°¾ */
        justify-content: flex-end;
    }
    article div {
        width: 80px;
        border: solid 5px blueviolet;
        text-align: center;
        font-size: 28px;
    }
</style>

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

ä½¿ç¨ `space-evenly` å¹³ååéå®¹å¨åç´ 

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/14.png)

```css
article {
    border: solid 5px silver;
    box-sizing: border-box;
    display: flex;
    flex-flow: row wrap;
    justify-content: space-evenly;
}
```

åç´æåæ¶å¯¹é½å°ä¸»è½´ç»ç¹

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/15.png)

```css
article {
    height: 400px;
    border: solid 5px silver;
    box-sizing: border-box;
    display: flex;
    flex-flow: column wrap;
    justify-content: flex-end;
}
```

### äº¤åè½´è¡ ð¾

ð åç´ å¨äº¤åè½´ä¸æè¡çæ¦å¿µï¼çè§£è¿ä¸ªæ¦å¿µä¼å¯¹çè§£align-itemsä¸align-contentææ´å¥½çå¸®å©ã

- align-itemæ¯æ§å¶åç´ å¨è¡ä¸çæå 
- align-contentæ¯æ§å¶è¡å¨äº¤å·®è½´ä¸çæåï¼åèjustify-contentï¼

<img src="https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/16.png" style="zoom:75%;" />

### align-items

ð ç¨äºæ§å¶å®¹å¨åç´ å¨äº¤åè½´(è¡)ä¸çæåæ¹å¼ã

| éé¡¹       | è¯´æ                             |
| :--------- | :------------------------------- |
| stretch    | åç´ è¢«æä¼¸ä»¥éåºå®¹å¨ï¼**é»è®¤**ï¼ |
| center     | åç´ ä½äºå®¹å¨çä¸­å¿               |
| flex-start | åç´ ä½äºå®¹å¨çäº¤åè½´å¼å¤´         |
| flex-end   | åç´ ä½äºå®¹å¨çäº¤åè½´ç»å°¾         |

**æä¼¸éåºäº¤åè½´**

ð å¦æè®¾ç½®äº `width | height | min-height | min-width | max-width | max-height` ï¼å°å½±å`stretch` çç»æãï¼stretchçä¼åçº§é«äºwidth/heightï¼

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/17.png)

```html
<style>
    * {
        padding: 0;
        margin: 0;
        padding: 10px;
        margin: 5px;
    }
    head {
        display: block;
    }
    body {
        font-size: 14px;
        color: #555;
    }
    article {
        height: 200px;
        border: solid 5px silver;
        box-sizing: border-box;
        display: flex;
        flex-direction: row;
        align-items: stretch;
    }
    article div {
        width: 80px;
        border: solid 5px blueviolet;
        text-align: center;
        font-size: 28px;
    }
</style>

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

**å¯¹é½å°äº¤åè½´çé¡¶é¨**

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/18.png)

```css
flex-direction: row;
align-items: flex-start;
```

**å¯¹é½å°äº¤åè½´åºé¨**

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/19.png)

```css
flex-direction: row;
align-items: flex-end;
```

**å¯¹é½å°äº¤åè½´ä¸­å¿**

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/20.png)

```css
flex-direction: row;
align-items: center;
```

çºµåæåæ¶äº¤åè½´æå

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/21.png)

```html
<style>
    * {
        padding: 0;
        margin: 0;
        padding: 10px;
        margin: 5px;
    }

    article {
        height: 400px;
        border: solid 5px silver;
        box-sizing: border-box;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    article div {
        height: 50px;
        min-width: 100px;
        border: solid 5px blueviolet;
        text-align: center;
        font-size: 28px;
    }
</style>

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

### align-content

ð åªéç¨äº**å¤è¡**æ¾ç¤ºçå¼¹æ§å®¹å¨ï¼ç¨äºæ§å¶è¡ï¼èä¸æ¯åç´ ï¼å¨äº¤åè½´ä¸çæåæ¹å¼ã

| éé¡¹          | è¯´æ                                                         |
| :------------ | :----------------------------------------------------------- |
| stretch       | å°ç©ºé´å¹³ååéç»åç´                                          |
| flex-start    | åç´ ç´§é ä¸»è½´èµ·ç¹                                             |
| flex-end      | åç´ ç´§é ä¸»è½´ç»ç¹                                             |
| center        | åç´ ä»å¼¹æ§å®¹å¨ä¸­å¿å¼å§                                       |
| space-between | ç¬¬ä¸ä¸ªåç´ é èµ·ç¹ï¼æåä¸ä¸ªåç´ é ç»ç¹ï¼ä½ä¸åç´ å¹³ååéç©ºé´   |
| space-around  | æ¯ä¸ªåç´ ä¸¤ä¾§çé´éç¸ç­ãæä»¥ï¼é¡¹ç®ä¹é´çé´éæ¯é¡¹ç®ä¸è¾¹æ¡çé´éå¤§ä¸å |
| space-evenly  | åç´ é´è·ç¦»å¹³ååé                                           |

**æ°´å¹³æåå¨äº¤åè½´ä¸­å±ä¸­æå**

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/22.png)

```html
<style>
    * {
        padding: 0;
        margin: 0;
        padding: 10px;
        margin: 5px;
    }
    article {
        height: 500px;
        border: solid 5px silver;
        box-sizing: border-box;
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        /* åè¡åçåç´ å¨å¤´é¨å¯¹é½ */
        align-items: flex-start;
        /* ææè¡é½å¨ä¸­é´æå */
        align-content: center;
    }
    article div {
        width: 90px;
        border: solid 5px blueviolet;
        text-align: center;
        font-size: 28px;
    }
</style>

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

**åç´æåæ¶äº¤åè½´çæå**

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/23.png)

```html
<style>
    * {
        padding: 0;
        margin: 0;
        padding: 10px;
        margin: 5px;
    }
    article {
        height: 300px;
        border: solid 5px silver;
        box-sizing: border-box;
        display: flex;
        flex-direction: column;
        flex-wrap: wrap;
        align-items: flex-start;
        /* ææåé½å¨ä¸­é´æå */
        align-content: center;
    }
    article div {
        min-width: 50px;
        min-height: 80px;
        border: solid 5px blueviolet;
        text-align: center;
        font-size: 28px;
    }
</style>

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

## å¼¹æ§åç´ 

::: tip æ¾å¨å®¹å¨çå­ä¸­çåç´ å³ä¸ºå®¹å¨åç´ ã

- ä¸è½ä½¿ç¨floatä¸clearè§å
- å¼¹æ§åç´ åä¸ºååç´ 
- ç»å¯¹å®ä½çå¼¹æ§åç´ ä¸åä¸å¼¹æ§å¸å±

:::

ð *ç»å¯¹å®ä½çå¤±å»äºåæ¥çææ¡£ä½ç½®ï¼èç¸å¯¹å®ä½çåç´ è¿ä¿çåæ¥çææ¡£ä½ç½®* 

### align-self

ð ç¨äºæ§å¶åä¸ªåç´ å¨**äº¤åè½´**ä¸çæåæ¹å¼ï¼`align-items` ç¨äºæ§å¶å®¹å¨ä¸­ææåç´ çæåï¼è `align-self` ç¨äºæ§å¶ä¸ä¸ªå¼¹æ§åç´ çäº¤åè½´æåã

| éé¡¹       | è¯´æ                   |
| :--------- | :--------------------- |
| stretch    | å°ç©ºé´å¹³ååéç»åç´    |
| flex-start | åç´ ç´§é ä¸»è½´èµ·ç¹       |
| flex-end   | åç´ ç´§é ä¸»è½´ç»ç¹       |
| center     | åç´ ä»å¼¹æ§å®¹å¨ä¸­å¿å¼å§ |

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/26.png)

```html
<style>
    * {
        padding: 0;
        margin: 0;
        padding: 10px;
        margin: 5px;
    }
    article {
        height: 400px;
        border: solid 5px silver;
        box-sizing: border-box;
        display: flex;
        flex-direction: row;
        align-items: center;
    }
    article div {
        height: 50px;
        min-width: 50px;
        border: solid 5px blueviolet;
        text-align: center;
        font-size: 28px;
    }
    article div:nth-of-type(1) {
        align-self: flex-start;
    }
    article div:nth-of-type(3) {
        align-self: flex-end;
    }
</style>

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

### flex-grow

ð ç¨äºå°å¼¹æ§çå­çå¯ç¨ç©ºé´ï¼åéç»å¼¹æ§åç´ ãå¯ä»¥ä½¿ç¨æ´æ°æå°æ°å£°æã

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/27.png)

```html
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        padding-left: 50px;
        padding-top: 15px;
    }

    article {
        border: solid 5px silver;
        width: 550px;
        height: 100px;
        display: flex;
        flex-direction: row;
    }

    article * {
        flex-grow: 1;
        width: 100px;
        height: 100px;
        background: blueviolet;
        background-clip: content-box;
        padding: 10px;
        box-sizing: border-box;
        font-size: 35px;
        color: white;
    }
</style>

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

å¦æå¼¹æ§åç´ è®¾ç½®äºå®½åº¦ï¼å°æï¼å¼¹æ§çå­-å¼¹æ§åç´ å®½åº¦åï¼åæç§ `flex-grow` è¿è¡åé ã

ä¸ä¾ä¸­ä¸ºä¸ä¸ªDIV å¼¹æ§åç´ è®¾ç½®äº1ã3ã6 ï¼å³å®½åº¦åæ10ç­ä»½ï¼ç¬¬ä¸ä¸ªåç´ æå å®½åº¦ä¸º`(å®½åº¦/(1+3+6)) X 6`ã

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/28.png)

```html
<style>
    * {
        padding: 0;
        margin: 0;
        padding: 10px;
        margin: 5px;
    }
    article {
        width: 600px;
        position: relative;
        height: 200px;
        border: solid 5px silver;
        display: flex;
    }
    article div {
        min-height: 80px;
        border: solid 5px blueviolet;
        text-align: center;
        font-size: 28px;
    }
    article div:nth-of-type(1) {
        width: 100px;
        flex-grow: 1;
    }
    article div:nth-of-type(2) {
        width: 100px;
        flex-grow: 3;
    }
    article div:nth-of-type(3) {
        width: 300px;
        flex-grow: 6;
    }
</style>
```

### flex-shrink

ð ä¸ `flex-grow` ç¸å `flex-shrink` æ¯å¨å¼¹æ§çå­è£ä¸ä¸åç´ æ¶å®ä¹ç**ç¼©å°å¼**ã

ä¸ä¾å¨600å®½çå¼¹æ§çå­ä¸­æ¾äº 1000 å®½çå¼¹æ§åç´ ãå¹¶ä¸ºæåä¸¤ä¸ªåç´ è®¾ç½®äºç¼©æ¾ï¼æåä¸ä¸ªåç´ çç¼©æ¾æ¯ä¾ä¸º 500 -( ( (1000-600) / (100X1+400x3+500X6) ) x 3 ) X 500 = 220.9ï¼è®¡ç®å¬å¼è¯´æå¦ä¸ï¼

```text
ç¼©å°æ¯ä¾ = ä¸è¶³çç©ºé´ / (åç´  1 å®½åº¦ x ç¼©å°æ¯ä¾) + (åç´  2 å®½åº¦ x ç¼©å°æ¯ä¾) ...
æç»å°ºå¯¸ = åç´ ä¸å®½åº¦ - (ç¼©å°æ¯ä¾ x  åç´  3 çå®½åº¦) X åç´ å®½åº¦
```

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/29.png)

```html
<style>
    * {
        padding: 0;
        margin: 0;
    }
    body {
        padding-left: 50px;
        padding-top: 15px;
    }
    article {
        border: solid 5px silver;
        width: 400px;
        height: 120px;
        display: flex;
        padding: 10px;
        box-sizing: content-box;
    }
    article div:nth-child(1) {
        flex-shrink: 0;
    }
    article div:nth-child(2) {
        flex-shrink: 1;
    }
    article div:nth-child(3) {
        flex-shrink: 3;
    }
    article * {
        width: 200px;
        height: 100px;
        overflow: hidden;
        background: blueviolet;
        background-clip: content-box;
        padding: 10px;
        border: solid 1px blueviolet;
        box-sizing: border-box;
        font-size: 30px;
        color: white;
    }
</style>

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

### flex-basis

ð flex-basis å±æ§å®ä¹äºå¨åéå¤ä½ç©ºé´ä¹åï¼é¡¹ç®å æ®çä¸»è½´ç©ºé´ï¼main sizeï¼ãæµè§å¨æ ¹æ®è¿ä¸ªå±æ§ï¼è®¡ç®ä¸»è½´æ¯å¦æå¤ä½ç©ºé´ã

å¯ä»¥æ¯é¿åº¦åä½ï¼ä¹å¯ä»¥æ¯ç¾åæ¯ã`flex-basis`çä¼åçº§é«äº`widthãheight`å±æ§ã

**ä¼åçº§**

flex-basis ä¼åçº§å¤§äº widthãheightã

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/30.png)

```html
<style>
    * {
        padding: 0;
        margin: 0;
    }
    article {
        width: 600px;
        position: relative;
        height: 150px;
        margin-left: 100px;
        margin-top: 100px;
        outline: solid 5px silver;
        display: flex;
        padding: 20px;
    }
    article div {
        outline: solid 5px blueviolet;
        text-align: center;
        font-size: 28px;
        line-height: 5em;
    }
    article div:nth-of-type(1) {
        flex-basis: 100px;
        width: 200px;
    }
    article div:nth-of-type(2) {
        flex-basis: 200px;
    }
    article div:nth-of-type(3) {
        flex-basis: 200px;
    }
</style>

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

### flex

ð flexæ¯flex-growãflex-shrink ãflex-basisç¼©åç»åã

> å»ºè®®ä½¿ç¨ flex é¢ä¸è¦åç¬ä½¿ç¨ flex-grow / flew-shrink / flex-basis ã

ä¸ä¾å®ä¹å¹³ååéå©ä½ç©ºé´ï¼å¹¶ä¸è¿è¡å°ºå¯¸ç¼©å°ï¼åºç¡å°ºå¯¸ä¸º200pxã

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/31.png)

```css
* {
    padding: 0;
    margin: 0;
}
article {
    width: 600px;
    position: relative;
    height: 150px;
    margin-left: 100px;
    margin-top: 100px;
    outline: solid 5px silver;
    display: flex;
    padding: 20px;
}
article div {
    outline: solid 5px blueviolet;
    text-align: center;
    font-size: 28px;
    line-height: 5em;
    /* stretch: 1(ç­æ¯å æ); strink: 0(ä¸ç¼©å°); 100px(åå§å¼) */
    flex: 1 0 100px;
}
```

### order

ð ç¨äºæ§å¶å¼¹æ§åç´ çä½ç½®ï¼é»è®¤ä¸º `order:0` æ°å¼è¶å°è¶å¨åé¢ï¼å¯ä»¥è´æ°ææ´æ°ã

ä¸é¢æ¯éè¿Jå¨ææ¹åorderå±æ§äº§çç§»å¨ææï¼å ä¸ºæ¬ç« èæ¯è®²CSSæä»¥JSåè½æ²¡æå®åï¼åªæ¯ä½éªä¸ä¸orderã

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/32.gif)

```html
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        padding-left: 50px;
        padding-top: 15px;
    }

    article {
        border: solid 5px silver;
        width: 400px;
        height: 400px;
        padding: 10px;
        display: flex;
        flex-direction: column;

    }

    article section {
        order: 1;
        flex: 1 0 100px;
        padding: 10px;
        background: blueviolet;
        background-clip: content-box;
        display: flex;
        flex-direction: column;
        text-align: center;
        color: white;
    }

    article section div {
        flex: 1;
    }

    article section div {
        display: flex;
        flex-direction: column;
        justify-content: center;
    }

    article section span {
        flex: 0;
        background: #000;
        padding: 20px;
        cursor: pointer;
    }
</style>

<article>
    <section>
        <div>content1</div>
        <span onclick="up(this)">up</span>
    </section>
    <section>
        <div>content2</div>
        <span onclick="up(this)">up</span>
    </section>
</article>

<script>
    function up(el) {
        el.parentElement.style.order = getOrder(el.parentElement) * 1 - 1;
        console.log(getOrder(el.parentElement))
    }

    function getOrder(el) {
        return getComputedStyle(el, null).order;
    }
</script>
```

## å¼¹æ§ææ¬

ææ¬èç¹ä¹å¨å¼¹æ§å¸å±æä½èå´åã

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/33.png)

```html
<style>
    article {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        height: 100vh;
        align-items: center;
        font-size: 14px;
    }
</style>

<article>
    hello
    <span> Michael </span>
    welcome !
</article>
```

## ç»å¯¹å®ä½

ç»å¯¹å®ä½çå¼¹æ§åç´ ä¸åä¸å¼¹æ§å¸å±ï¼ç»å¯¹å®ä½çåç´ å·²ç»å¤±å»äºåå§çææ¡£ä½ç½®ï¼èç¸å¯¹å®ä½ä¿æï¼

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/34.png)

```html
<style>
    * {
        padding: 0;
        margin: 0;
        padding: 10px;
        margin: 5px;
    }
    article {
        position: relative;
        height: 400px;
        border: solid 5px silver;
        box-sizing: border-box;
        display: flex;
        justify-content: space-evenly;
        align-items: flex-start;
    }
    article div {
        min-width: 50px;
        min-height: 80px;
        border: solid 5px blueviolet;
        text-align: center;
        font-size: 28px;
    }
    article div:nth-of-type(1) {
        position: absolute;
        top: 0;
    }
</style>

<article>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</article>
```

## å¾®ä¿¡å¬ä¼å·

ä¸é¢æ¥å¼åç±»ä¼¼å¾®ä¿¡å¬ä¼å·å¸å±ï¼åæ¬åºé¨äºçº§èåçå¼¹æ§å¸å±ã

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/35.png)

```html
<style>
    * {
        padding: 0;
        margin: 0;
    }

    body {
        display: flex;
        flex-direction: column;
        height: 100vh;
        color: #666;
    }

    main {
        flex: 1;
    }

    footer {
        height: 50px;
        background: blueviolet;
        display: flex;
        justify-content: space-evenly;
    }

    footer section {
        display: flex;
        flex: 1 0;
        flex-direction: column-reverse;
        border-right: solid 1px #555;
        border-top: solid 1px #555;
    }

    footer section:last-child {
        border-right: none;
    }

    footer section h4 {
        flex: 0 0 50px;
        display: flex;
        text-align: center;
        flex-direction: column;
        justify-content: center;
        cursor: pointer;
        color: white;
    }

    footer section ul {
        text-align: center;
        display: flex;
        flex-direction: column;
        border: solid 1px #555;
        margin-bottom: 5px;
        border-radius: 5px;
        margin: 5px;
    }

    footer section ul li {
        flex: 1 0 50px;
        border-bottom: solid 1px #555;
        display: flex;
        flex-direction: column;
        justify-content: center;
        cursor: pointer;
    }

    footer section ul li:last-child {
        border: none;
    }
</style>
...

<main></main>
<footer>
    <section>
        <h4>æç¨</h4>
        <ul>
            <li>PHP</li>
            <li>LINUx</li>
        </ul>
    </section>
    <section>
        <h4>ç´æ­</h4>
    </section>
</footer>
```

## èªå¨ç©ºé´

å¨å¼¹æ§å¸å±ä¸­å¯¹åç´ ä½¿ç¨`margin-right:auto` ç­å½¢å¼å¯ä»¥èªå¨ææ»¡ç©ºé´ãä¸ä¾ä¸ºç¬¬ä¸ä¸ªulè®¾ç½® `margin-right:auto` è¡¨ç¤ºå³ä¾§ç©ºé´èªå¨ææ»¡ï¼ç¬¬äºä¸ªulé è¿ç¶åç´ å³è¾¹çãï¼`flex: 1`ä¹å¯ä»¥è¾¾å°è¿ä¸ªææï¼

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/css/flex/36.png)

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        .container {
            width: 1200px;
            margin: 0 auto;
        }

        nav {
            display: flex;
            border: solid 1px green;
            margin-top: 20px;
            align-items: center;
            height: 60px;
            box-shadow: 0 0 5px rgba(0, 0, 0, .2);
            background: #f3f3f3;
        }

        ul {
            list-style: none;
        }

        ul:nth-child(1) {
            display: flex;
            align-items: center;
            margin-right: auto;
        }

        ul:nth-child(1)>li {
            margin: 0 10px;
        }

        ul:nth-child(2)>li {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: #9b59b6;
        }
    </style>
</head>

<body>
    <div class="container">
        <nav>
            <ul>
                <li>ææ¡£</li>
                <li>æç¨</li>
                <li>è§é¢</li>
                <li>äº¤æµ</li>
            </ul>
            <ul>
                <li>
                </li>
            </ul>
        </nav>
    </div>
</body>
```