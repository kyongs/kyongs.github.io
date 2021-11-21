---
title: "[CSS] rem, em 차이점"
updated: 2021-11-21 15:15
---

## em

해당 단위가 사용되고 있는 요소의 font-size 속성 값이 기준이 됨<br/>
`참고로 브라우저 기본 폰트 크기는 보통 16px이다`<br/><br/>
ex)

```css
html {
  font-size: 16px;
}
div {
  font-size: 20px;
  width: 10em; /* ===> 20 * 10 = 200px*/
}
```

## rem

최상위 요소(root)의 font-size 속성 값이 됨
ex)

```css
html {
  font-size: 16px;
}
div {
  font-size: 20px;
  width: 10rem; /* ===> 16 * 10 = 160px*/
}
```
