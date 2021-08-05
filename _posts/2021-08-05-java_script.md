---
last_modified_at : 2021-08-05
layout: single
title:  "Java script test"
categories: blog
tags: [java script, JS]

toc: true
toc_sticky: true
---
## 서론
지킬로 만든 홈페이지 안에 자바스크립트를 넣을 수 있을까요?

## Test
<input type="button" id='hw' value='hello world'>
<script>
    var hw = document.getElementById('hw');
    hw.addEventListener('click', function () {
        alert('hello world')
    })
</script>
