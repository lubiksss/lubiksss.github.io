---
last_modified_at : 2021-07-14
title:  "Github README.md에 Latex수식 넣기"
categories: github
tags : [latex, markdown]
---
markdown 렌더링시 mathjax를 사용할 수 있는 경우는 mathjax를 사용하여 수식을 작성할 수 있지만 github의 README.md는 mathjax를 사용하지 않습니다. 따라서 아래와 같은 방법으로 이미지 형태의 latex 수식을 넣어줄 수 있습니다.  
<a href='http://www.codecogs.com/latex/eqneditor.php'>http://www.codecogs.com/latex/eqneditor.php</a>  
위 페이지에 접속해서 latex 문법으로 수식을 적고 페이지 제일 아래 항목을 URL encoded로 복사합니다.
```markdown
![대체텍스트](이미지주소 "이미지 제목")
```
위와 같은 형식으로 적으면 markdown에 latex 수식 이미지를 포함시킬 수 있습니다.
아래는 이 포스트에 적용한 결과입니다. 포스트도 md 파일이니 github에서도 똑같이 적용됩니다.

```latex
c = \sum_{(A_i^I,v_i^I)\in I}v_i^I -  \sum_{(A_j^O,v_j^O)\in O}v_j^O
```
```markdown
![equation](https://latex.codecogs.com/gif.latex?%5Chuge%20c%20%3D%20%5Csum_%7B%28A_i%5EI%2Cv_i%5EI%29%5Cin%20I%7Dv_i%5EI%20-%20%5Csum_%7B%28A_j%5EO%2Cv_j%5EO%29%5Cin%20O%7Dv_j%5EO)
```
![equation](https://latex.codecogs.com/gif.latex?%5Chuge%20c%20%3D%20%5Csum_%7B%28A_i%5EI%2Cv_i%5EI%29%5Cin%20I%7Dv_i%5EI%20-%20%5Csum_%7B%28A_j%5EO%2Cv_j%5EO%29%5Cin%20O%7Dv_j%5EO){: .center}

![equation](https://latex.codecogs.com/gif.latex?%5Cbg_white%20%5Chuge%20c%20%3D%20%5Csum_%7B%28A_i%5EI%2Cv_i%5EI%29%5Cin%20I%7Dv_i%5EI%20-%20%5Csum_%7B%28A_j%5EO%2Cv_j%5EO%29%5Cin%20O%7Dv_j%5EO){: .center}

![equation](https://latex.codecogs.com/gif.latex?%5Cbg_black%20%5Chuge%20c%20%3D%20%5Csum_%7B%28A_i%5EI%2Cv_i%5EI%29%5Cin%20I%7Dv_i%5EI%20-%20%5Csum_%7B%28A_j%5EO%2Cv_j%5EO%29%5Cin%20O%7Dv_j%5EO){: .center}

![equation](https://latex.codecogs.com/gif.latex?%5Cbg_gray%20%5Chuge%20c%20%3D%20%5Csum_%7B%28A_i%5EI%2Cv_i%5EI%29%5Cin%20I%7Dv_i%5EI%20-%20%5Csum_%7B%28A_j%5EO%2Cv_j%5EO%29%5Cin%20O%7Dv_j%5EO){: .center}

투명 배경일 때 글씨색을 하얀색으로 제공해주지 않아서 블랙모드에서는 가독성이 떨어져서 못 쓰고 배경을 검은색으로 하면 잘 보입니다.  
github 이미지 업로드 관련 다른게 궁금하시면 아래 블로그 참고하시면 됩니다.
<a href = 'https://blog.yena.io/studynote/2017/11/23/Github-resize-image.html'>https://blog.yena.io/studynote/2017/11/23/Github-resize-image.html<a>
