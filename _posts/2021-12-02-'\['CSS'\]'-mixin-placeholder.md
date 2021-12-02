---
title: "[CSS] mixin, placeholder 차이점"
updated: 2021-12-02 16:55
---

## mixin

매개변수 받을 수 있음<br/>
여기저기서 다 가져다 쓸 수 있음<br/>

ex)

```scss
@mixin responsive($screen) {
  @if ($screen == "T") {
    @media screen and (min-width: $md-breakpoint) {
      @content;
    }
  }

  @if ($screen == "D") {
    @media screen and (min-width: $lg-breakpoint) {
      @content;
    }
  }
}
```

## placeholder

매개변수 받을 수 없음<br/>
확장성이 떨어짐<br/>
연관된 애들끼리 공통된 스타일을 가지고 있을 때 placeholder 설정 후 상속받아 사용<br/>

ex)

```scss
%tag-base {
  //공통 스타일
  @include inline-flexbox;
  @include text-style(12);

  height: 20px;
  padding: 0 6px;
  font-weight: 700;
  border-radius: 4px;
}

.tag-red {
  @extend %tag-base;
}
```
