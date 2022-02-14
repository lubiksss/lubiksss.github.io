---
last_modified_at : 2021-08-05
layout: single
title:  "Java script test"
categories: blog
tags: [JS, java script]

toc: true
toc_sticky: true
---
## 서론
지킬로 만든 홈페이지 안에 자바스크립트를 넣을 수 있을까요?

## Test
<input type="button" id='hw' value='click me' style='background: #505050'>
잘 들어가는 것 같습니다.
<script>
    var hw = document.getElementById('hw');
    hw.addEventListener('click', function () {
        alert('hello world')
    })
</script>
