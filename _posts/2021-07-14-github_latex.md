---
last_modified_at : 2021-07-14
title:  "Github README.md에 Latex수식 넣기"
categories: github
tags : [latex, markdown]
---
<a href='http://www.codecogs.com/latex/eqneditor.php'>http://www.codecogs.com/latex/eqneditor.php</a>  
이 페이지에 접속해서 latex 수식을 적고 페이지 제일 아래 항목을 URL encoded로 복사합니다.
```markdown
![equation](복사한값)
```
위와 같은 형식으로 적으면 markdown에 latex수식을 포함시킬 수 있습니다.
아래는 이 포스트에 적용한 결과입니다.

```markdown
![equation](https://latex.codecogs.com/gif.latex?c%20%3D%20%5Csum_%7B%28A_i%5EI%2Cv_i%5EI%29%5Cin%20I%7Dv_i%5EI%20-%20%5Csum_%7B%28A_j%5EO%2Cv_j%5EO%29%5Cin%20O%7Dv_j%5EO)
```
>![equation](https://latex.codecogs.com/gif.latex?c%20%3D%20%5Csum_%7B%28A_i%5EI%2Cv_i%5EI%29%5Cin%20I%7Dv_i%5EI%20-%20%5Csum_%7B%28A_j%5EO%2Cv_j%5EO%29%5Cin%20O%7Dv_j%5EO)
