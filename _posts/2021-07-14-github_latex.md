---
last_modified_at : 2021-07-14
layout : single
title:  "Github README.md에 Latex수식 넣기"
categories: github
tags : [latex, markdown]

toc: true
toc_sticky: true
---
## 서론
markdown 렌더링 시 mathjax를 사용할 수 있는 경우는 mathjax를 사용하여 수식을 작성할 수 있지만 github의 README.md는 mathjax를 사용하지 않습니다. 따라서 아래와 같은 방법으로 github의 README.md에 이미지 형태의 latex 수식을 넣어야 합니다.

## 수식 넣기
아래와 같은 형식으로 적으면 markdown에 latex 수식 이미지를 포함시킬 수 있습니다.
```markdown
![대체텍스트](이미지주소 "이미지 제목")
```
<a href='http://www.codecogs.com/latex/eqneditor.php'>http://www.codecogs.com/latex/eqneditor.php</a>  
적어야 할 주소는 위 페이지에 접속해서 latex 문법으로 수식을 적고 페이지 제일 아래 항목을 URL encoded로 복사하면 얻을 수 있습니다. 아래는 사용한 latex 수식입니다.
```latex
c = \sum_{(A_i^I,v_i^I)\in I}v_i^I -  \sum_{(A_j^O,v_j^O)\in O}v_j^O
```
<br>
아래는 이 포스트에 실제로 적은 코드와 적용한 결과입니다. 포스트도 md 파일이니 github README.md에서도 똑같이 적용됩니다.
```markdown
![equation](https://latex.codecogs.com/gif.latex?%5Cbg_black%20%5Chuge%20c%20%3D%20%5Csum_%7B%28A_i%5EI%2Cv_i%5EI%29%5Cin%20I%7Dv_i%5EI%20-%20%5Csum_%7B%28A_j%5EO%2Cv_j%5EO%29%5Cin%20O%7Dv_j%5EO)
```
![equation](https://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Chuge%20c%20%3D%20%5Csum_%7B%28A_i%5EI%2Cv_i%5EI%29%5Cin%20I%7Dv_i%5EI%20-%20%5Csum_%7B%28A_j%5EO%2Cv_j%5EO%29%5Cin%20O%7Dv_j%5EO){: .center}

![equation](https://latex.codecogs.com/gif.latex?%5Cbg_gray%20%5Chuge%20c%20%3D%20%5Csum_%7B%28A_i%5EI%2Cv_i%5EI%29%5Cin%20I%7Dv_i%5EI%20-%20%5Csum_%7B%28A_j%5EO%2Cv_j%5EO%29%5Cin%20O%7Dv_j%5EO){: .center}

![equation](https://latex.codecogs.com/gif.latex?%5Cbg_black%20%5Chuge%20c%20%3D%20%5Csum_%7B%28A_i%5EI%2Cv_i%5EI%29%5Cin%20I%7Dv_i%5EI%20-%20%5Csum_%7B%28A_j%5EO%2Cv_j%5EO%29%5Cin%20O%7Dv_j%5EO){: .center}
