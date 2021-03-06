
# 정기 보고서 자동 작성을 위해 knitr로 문서화하고 스케줄러로 자동화하기 {#knitr}

## Markdown 문법 {#markdown}

### 마크다운이란 {#markdown-exp}

[마크다운][803]이란 `plain text`를 쉽게 일정 양식의 문서로 바꿀 수 있게 간단한 규칙을 정해 놓은 것을 말합니다. 문서의 디자인을 결정하는 요소는 발달 과정에 따라 `html`을 대표로 일정 표준이 만들어지고 관리되고 있습니다. `html`과 `css`는 웹페이지가 어떻게 보이는지를 결정하는 문법으로 구성되어 있습니다. `html`은 문서를 구조화하여 같은 상태로 둘 요소들을 같은 상태로 표기하는 것이고, `css`는 그 같은 조건에 있는 것들을 같은 모양으로 보이게, 모양을 작성하는 문서입니다. 그렇기 때문에 `html`의 요소들을 잘 정의했으면, `css`에 따라 마치 테마가 바뀌는 것처럼 따라 바꿀 수 있게 됩니다.    
그 중 문서에 필요한 최소한의 `markdown` 규칙을 [commonmark][803]에서 지정을 했구요. 너무 단순한 규칙 때문에 매우 많은 확장 문법들이 각자의 방식으로 발전했습니다. 특히 오픈소스의 발달로 소스에 대한 설명 등이 `plain text` 양식으로, `README` 라는 이름의 파일로 남기는 것이 관례가 되었습니다. 소스 관리 저장소 서비스를 운영하는 `github` 같은 곳에서는 웹으로 서비스를 제공하고 있고, 이 `plain text`를 예쁘게 보여주기 위해서 `markdown`문법을 채택했으며 각 서비스 들이 각자 추가적인 문법을 제공하고 있는 중입니다. 현재 `0.27`버전이 정리가 되었고 [이곳][807]에서 확인하실 수 있습니다.

### 문법 소개 {#syntax}

`markdown`이 down인 만큼 `html`에서 구조화를 위해 사용하는 요소들을 사용할 수 있습니다.

```
제목 : # , =====
인용 : >
강조 : * , _
링크 : [텍스트](주소 "설명 생략가능")
이미지 : ![텍스트](이미지주소 "설명 생략가능")
리스트 : 1 , * , - , +
코드표시 : <code>코드</code> , 한줄 띄우고 스페이스 4칸 , ```코드```
줄바꿈 : 엔터 2번 , 강제 줄바꿈은 문장끝에 스페이스바 2칸
가로선 : ----- , ***** , +++++

```

#### 제목

`#`이 표시가 `html`에서는 `<h1>` 태그와 같습니다. `<h>`는 총 6까지 있으며 `#`표시는 숫자를 쓰는게 아니라 `#` 갯수로 수를 표현합니다.

```
# 제목1 : HTML의 <h1> 태그
## 제목2 : HTML의 <h2> 태그
### 제목3 : HTML의 <h3> 태그
#### 제목4 : HTML의 <h4> 태그
##### 제목5 : HTML의 <h5> 태그
###### 제목6 : HTML의 <h6> 태그
```

#### 인용

인용은 인용 속에 인용, 인용 속에 인용이 가능한 구조입니다. 보통 왼쪽에 세로줄이 있는 형태로 뫼부에 보여줍니다. 

```
> ### 제일 바깥의 인용
>> ** 인용의 인용 **
```
> ### 제일 바깥의 인용
>> ** 인용의 인용 **

#### blod & italic

강조하는 방식은로는 `*` 이나 `_`의 갯수로 결정납니다.

```
이것은 **굵은 글씨** 입니다.
이것은 __굵은 글씨__ 입니다.

이것은 *기울여 쓰기* 입니다.
이것은 _기울여 쓰기_ 입니다.

이것은 ***강조하며 기울여 쓰기*** 입니다.
이것은 ___강조하며 기울여 쓰기___ 입니다.
```

이것은 **굵은 글씨** 입니다.  
이것은 __굵은 글씨__ 입니다.

이것은 *기울여 쓰기* 입니다.  
이것은 _기울여 쓰기_ 입니다.

이것은 ***강조하며 기울여 쓰기*** 입니다.  
이것은 ___강조하며 기울여 쓰기___ 입니다.


#### links

바로가기 링크를 페이지상에 바로 구현할 수 있습니다. 링크를 바로 옆에 작성하는 방식과 주석처럼 다는 2가지 방식이 있습니다. 앞에서 사용한 방식을 인라인 방식이라고 하고, 뒤에 방식을 레퍼런스 방식이라고 합니다.

```
이것은 [링크](http://www.example.com) 입니다.
이것은 [링크](http://www.example.com "설명문구 생략가능") 입니다.
이것은 [구글 링크][1] 입니다.
이것은 [마이크로소프트 링크][b] 입니다.
이것은 [애플 링크][three] 입니다.
 
[1]: https://www.google.co.kr "구글"
[b]: https://www.microsoft.com/ko-kr/ "마이크로소프트"
[three]: http://www.apple.com/kr/ "애플"

```

이것은 [링크](http://www.example.com) 입니다.
이것은 [링크](http://www.example.com "설명문구 생략가능") 입니다.
이것은 [구글 링크][1] 입니다.
이것은 [마이크로소프트 링크][b] 입니다.
이것은 [애플 링크][three] 입니다.
 
[1]: https://www.google.co.kr "구글"
[b]: https://www.microsoft.com/ko-kr/ "마이크로소프트"
[three]: http://www.apple.com/kr/ "애플"

#### image

이미지를 첨부하는 방법은 마우스를 사용하는 방식이 아니라서 좀 불편할 수 있습니다. 앞서 바로가기 링크를 만드는 것과 같은 방식인데 앞에 `!`를 추가해서 작성합니다. 이미지는 실제로 문서에서 해당 링크의 이미지를 가져와서 문서에서 보여주는 방식입니다. 이미지의 위치나 크기 같은 것을 조정하기 위해서는 기본 markdown 문법에서는 제공하지 않습니다. 그래서 관련 문법을 제공하는 서비스를 사용하거나 `html` 문법이나 `css` 를 사용해야 합니다.

```
1. ![깃헙](https://upload.wikimedia.org/wikipedia/commons/thumb/2/29/GitHub_logo_2013.svg/225px-GitHub_logo_2013.svg.png "설명문구 생략가능")
2. ![깃허브][imgGithub]
 
[imgGithub]: https://upload.wikimedia.org/wikipedia/commons/thumb/2/29/GitHub_logo_2013.svg/225px-GitHub_logo_2013.svg.png "설명문구 생략가능"

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/29/GitHub_logo_2013.svg/225px-GitHub_logo_2013.svg.png" width="200">

```
1. ![깃헙](https://upload.wikimedia.org/wikipedia/commons/thumb/2/29/GitHub_logo_2013.svg/225px-GitHub_logo_2013.svg.png "설명문구 생략가능")
2. ![깃허브][imgGithub]
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/29/GitHub_logo_2013.svg/225px-GitHub_logo_2013.svg.png" width="200">
 
[imgGithub]: https://upload.wikimedia.org/wikipedia/commons/thumb/2/29/GitHub_logo_2013.svg/225px-GitHub_logo_2013.svg.png "설명문구 생략가능"

#### number

앞에 숫자를 붙여서 작업하고 싶을 때가 있습니다. `1. ` 를 앞에 입력하시면 들여쓰기가 같은 줄에 따라 숫자를 붙여줍니다. 숫자를 자유롭게 사용하셔도 순서대로 작업해주니 보통 1로만 작성하는 것 같습니다. 들여쓰기는 4칸 띄어쓰기를 의미합니다. 

```
1. 번호1
1. 번호2
    1. 번호1
    1. 번호2
    1. 번호3
1. 번호3
  1. 번호3
9. 번호5
```
1. 번호1
1. 번호2
    1. 번호1
    1. 번호2
    1. 번호3
1. 번호3
  1. 번호3
9. 번호 9

#### list

숫자 붙이는 것과 같이 앞에 동그라미 표시 등을 통해서 간결한 문체로 작성할 때가 있습니다. 들여쓰기로 3단까지 다른 모양을 자동으로 보여줍니다.
```
* 리스트 *
    * 리스트 *
    - 리스트 -
* 리스트 *
  - 리스트 -
  
* 리스트 *
    - 리스트 -
        - 리스트 -
            - 리스트 -
```
* 리스트 *
    * 리스트 *
    - 리스트 -
* 리스트 *
  - 리스트 -

* 리스트 *
    - 리스트 -
        - 리스트 -
            - 리스트 -


#### 코드

코드는 복사하기 좋고, 텍스트 그대로를 문서에 남길때 사용합니다. 위에 복사를 위한 글자들 모두 코드를 작성하는 양식으로 작성하였습니다. 아래에는 코드 안에 내용을 보이게 하기위해서 앞에 `" `를 붙여서 작성했습니다. souce를 직접 확인해 보시면 좋습니다.

```
" ```
코드 
" ```
```

```
코드
```

#### 수식

[LaTex][805]는 수식을 입력하는 규칙이 규정되어 있습니다. 이를 활용해서 `$$ 수식문법 $$` 의 규칙으로 복잡한 수식을 작성할 수 있습니다. 수식문법에 대해서는 좋은 [포스트][806]를 공유하니 추가적으로 필요하신 분들은 공부해보시면 좋을 것 같습니다.

```
$$
\left|\sum_{i=1}^n a_ib_i\right|
\le
\left(\sum_{i=1}^n a_i^2\right)^{1/2}
\left(\sum_{i=1}^n b_i^2\right)^{1/2}
$$
```
$$
\left|\sum_{i=1}^n a_ib_i\right|
\le
\left(\sum_{i=1}^n a_i^2\right)^{1/2}
\left(\sum_{i=1}^n b_i^2\right)^{1/2}
$$

## Rmd 양식으로 문서 작성 {#rmd}

`rmarkdown`는 위에서 설명한 `markdown`문법을 활용하여 R의 명령문과 조합해서 문서를 작성하기 위한 하나의 양식입니다. 공식 홈페이지는 [이곳][808]이고 소스는 [이 곳][804]을 확인하시면 됩니다. [한글 cheatsheet][801]도 있고, rstudio > help > cheatsheet 에도 [cheatsheet][810]과 [reference][809]가 있습니다.

`rmarkdown` 패키지는 `Rmd` 양식의 문서를 `knitr`과 `pandoc`으로 다양한 문서양식으로 생성해주는 패키지입니다.

![proccess](http://rmarkdown.rstudio.com/lesson-images/RMarkdownFlow.png)

`knitr`은 `rmd`양식의 문서 중 R엔진의 처리가 필요한 계산과 이미지 생성등의 작업을 자동화하여 `md`의 문법과 위치에 맞게 `md`문서를 생성해 줍니다. 그리고 `pandoc`이 [YAML][815]양식의 해더 정보를 바탕으로 다른 포멧의 저작물로 변환해주는 것입니다. [변환 가능한 저작물][814]로는 notebook, html, pdf, word, odt등의 문서와 ioslides, reveal.js, Slidy, Beamer의 슬라이드, 대쉬보드, 웹페이지, 책 등 입니다.

본 자료에서는 md와는 다르게 동작하는 rmd의 특수 문법들과 옵션을 알아보고, 각 문서형으로 변환하는 작업에 대해서 알아보겠습니다.

### R code 실행 결과

`Rmd`의 가장 강력한 점은 코드의 결과를 옮겨적거나 따로 저장해서 고쳐내지 않고, 최종 결과물을 코드에서 바로 작성할 수 있다는 점입니다. `Rmd`의 R 코드 실행시 변환해주는 내용은 아래 5가지 입니다.


```r
if(!require(knitr)) install.packages("knitr")
#> 필요한 패키지를 로딩중입니다: knitr
library(knitr)
obj<-c("소스코드","텍스트","플롯","메세지","경고")
role<-c("코드청크에 들어있는 R 코드",
        "summary(iris)와 같은 글자 출력 결과물",
        "plot(iris)와 같은 그림 출력 결과물",
        "메세지","경고")
dat<-data.frame("객체"=obj,"목적"=role)
kable(dat,align="cl")
```



   객체     목적                                  
----------  --------------------------------------
 소스코드   코드청크에 들어있는 R 코드            
  텍스트    summary(iris)와 같은 글자 출력 결과물 
   플롯     plot(iris)와 같은 그림 출력 결과물    
  메세지    메세지                                
   경고     경고                                  

코드 작성 방식은 `inline`과 `chunk` 방식으로 나뉩니다. `inline`은 글들과 함께 중간에 들어가는 것을 뜻하고, `chunk`는 말 그대로 코드 덩어리 째로 들어가서 위의 6가지를 출력할 것인지 말것인지의 옵션에 따라 결과물을 보여줍니다.

#### line R code

글자들 사이에 만약 항상 문서를 생성하는 시점의 날짜로 지정하고 싶다면 아래와 작성하면 됩니다.    
본 문서는 2017-08-20 에 작성되었습니다.    
소스를 확인해서 어떻게 작성했는지 확인해보세요.

#### code chunk

`chunk`는 `덩어리`라는 뜻 답게 코드가 실행되는 하나의 단위입니다. `Rmd`은 컴퓨터에 설치만 되어 있다면 다른 언어들도 `chunk`내의 실행 결과를 변환해서 `md`파일로 바꿔줍니다. `R`과 다른 점은 각 `chunk`별로 독립적인 프로세스를 실행시키기 때문에 변수들이 `chunk` 사이에서 함께 사용할 수 없습니다. 원래 코드를 작성하는 방식인 ```의 사이에 code를 작성하면 되는데 윗줄의 표시 뒤에 {R}을 작성하면 R 엔진으로 실행시킬 코드라는 사실을 knitr의 렌더링 함수가 이해하게 됩니다.

##### 출력 옵션들

위에 5개 내용에 대해서 `fig.cap`을 빼고 모두 `TRUE/FALSE`로 출력할지 말지 조정할 수 있습니다.
```
echo    : 코드
include : 코드와 글자 출력물
fig.cap : 그림 출력물
message : 메세지
warning : 경고
```

각 옵션은 `chuck`에게 `R`로 처리함을 알려주는 {R} 안에 작성합니다. 앞에 `"`는 제거해야 합니다.
```
"```{r echo=T}
"```{r echo=T, message=F}
"```{r echo=T, message=F,warning=F}
```

`fig.cap`은 그림 출력물의 가로 세로 길이나 위치 등의 옵션을 조정할 수 있습니다.

### YAML 해더를 이용한 출력물

#### YAML 해더

`Rmd` 초기 설명에 잠깐 언급한 `YAML` 해더에 대해서 설명하겠습니다. 이것에 따라서 html, word 등 출력 결과물을 조절할 수 있습니다.
```
---
title: 테스트 해더
author: 박찬엽
date: 2017년 5월
output: html_document
---
```

첫 양식인 `html`을 하기 위해서는 위와 같이 `output` 옵션을 `html_document`로 지정하면 됩니다. 그러면 해더 정보를 바탕으로 `html` 문서로 변환을 해줍니다. `html` 문서로 변환하는 것의 가장 큰 장점은 역시 동적 문서 형식을 유지할 수 있다는 점입니다 `PDF`나 `word`는 정적 문서이기 때문에 제한 된 기능으로만 출력물을 저장할 수 있습니다. `Rmd`에 동적 출력 결과물이 code상에 실행하도록 되어 있다면 `PDF`나 `word`로 변환시 에러를 일으킵니다. [webshot][816]은 본래 웹페이지를 기계적으로 스크린샷하기 위해 작성된 패키지인데, 문서중 동적인 요소들을 스크린샷해서 반영해주는 동작을 해줍니다. 

특별히 해더에 정보를 추가해서 디자인이나 테마를 변경할 수 있습니다. `html`은 이미 많은 [style][802]을 미리 지정해두고 이름만으로 사용할 수 있게 되어있습니다. [style][802]에서 지정해볼 수 있는 다른 테마들을 찾아보세요.
```
---
title: 테스트 해더
author: 박찬엽
date: 2017년 5월
output: 
  html_document:
    theme: flatly
---
```




`css`를 추가하려면 아래와 같이 작성합니다.
```
---
title: 테스트 해더
author: 박찬엽
date: 2017년 5월
output: 
  html_document:
    css: css/customStyle.css
---
```

위와 같이 작성하고 css 오른쪽에 디자인에 해당하는 css 파일의 경로를 지정해주면 됩니다. 

#### YAML params

`YAML`이 데이터 양식이라고 설명을 드렸습니다. 그래서 `Rmd`내부에서 접근할 수 있는 데이터를 `params`라는 이름으로 미리 작성해 둘 수 있습니다. 지금은 inline 코드를 양쪽에 `-`로 처리 했습니다.
```
---
title: -r params$chapter- 테스트 해더
params:
  chapter: 5
author: 박찬엽
date: 2017년 5월
output: 
  html_document:
    css: css/customStyle.css
---
```

해더 내 양식으로 보여드리려고 위와 같이 작성했지만 `Rmd` 문서 모든 `code` 작성 공간에서 같은 양식으로 값에 접근할 수 있습니다.


#### word 문서로 만들기

`Rmd`는 `word` 문서로도 변환할 수 있습니다. 위에서 설명한 `html_document` 위치에 `word_document` 라고 입력하면 됩니다. `word`에서는 스타일을 `word`문서에서 참조하는 방법이 있어 소개하려고 합니다.

##### reference docx 사용하기

1. 우선 `Rmd`를 `word` 출력물로 설정해서 새로 만듭니다. 그리고 knit 버튼을 이용해 우선 `docx` 확장자의 `word` 문서를 만듭니다. 그냥 새 파일을 만들수도 있지만, 호환이 잘 안되는 경우도 있어서 안전한 방법을 설명했습니다.

2. 만들어진 워드 파일을 새로운 이름으로 바꿔 저장합니다. 이번 예시에서는 `style.docx`로 저장했습니다. 

3. 저장된 `style.docx` 파일을 열어서 스타일 정보를 수정합니다. 확인하셔야 할 부분은 수정해야될 정보가 스타일이지, 각 텍스트 들의 디자인이 아니라는 점입니다.

4. 스타일 정보를 `YAML` 해더에 아래와 같이 입력해 줍니다. 
```
---
title: 워드 스타일 테스트 해더
author: 박찬엽
date: 2017년 5월
output: 
  word_document:
    reference_docx: style.docx
---
```
파일의 경로는 `Rmd` 파일이 있는 폴더의 위치가 `working diractory`라고 인식하므로 같은 곳에 있으면 추가적인 경로 작성 없이 위와 같이 파일 이름만 작성해 주면 됩니다. `word_style.Rmd`에 가능한 한 보이는 양식들을 넣은 기본 문서로 작성했으니 이 것으로 `word`문서를 생성후 스타일 파일로 사용하시면 좋을 것 같습니다.


#### PDF 문서로 만들기

PDF 문서로 만들 때는 위에 잠시 나왔던 LaTex이 설치되어 있어야 합니다. [이곳][817]에서 각자의 운영체제에 맞게 다운 받아 설치하시면 됩니다. `linux`는 기본 설치 되어 있을 텐데 콘솔에서 `latex`을 입력해보시면 됩니다. 없으면 debian 계열 `sudo apt-get install texlive`, Centos 계열 `sudo yum install tetex`로 설치할 수 있습니다.

PDF는 `word_document` 부분을 `pdf_document`라고 하면 됩니다. `?pdf_document`를 입력해서 설정할 수 있는 것이 무엇이 있는지 확인해 보세요.

한글 때문에 폰트 및 추가로 설정해야 하는 부분이 있습니다. [여기][818]와 [여기][819]를 참고하세요.



## 스케줄러 {#scheduler}

운영체제에 포함되어 있는 스케줄러란 일정한 시간이나 조건에 반복적으로 작업을 수행하게 해주는 프로그램입니다. 어떤 언어에서든 계속적인 작업을 위해서 스케줄러를 사용하는데, 아래는 대표적으로 사용하는 스케줄러를 소개하고 있습니다.

특히 환경변수라고 하는 부분에 대해서 `rstudio`의 작업환경과 조금 다르고, 분리해서 생각해야 할 부분이 있어서 조금 골치 아프기도 합니다. 운영체제에 특화되서 사용하기도 합니다. 윈도우는 내장되어 있는 작업 스케줄러, 리눅스 계열과 mac은 전통적으로 `cron`을 사용하고 있습니다. 서버에 일을 시키기 위해서 `cron`을 사용하는 방법을 익히는 것은 매우 중요한 것 같습니다.

### windows 작업 스케줄러 {#taskscheduler}

윈도우는 실행 파일을 정해진 시간에 자동으로 실행시켜주는 `task scheduler`가 있습니다. 이것을 컨트롤하는 패키지인 [taskscheduleR][820]가 있어서 함께 사용해 보겠습니다.

### linux 작업 스케줄러 {#crontab}

`cron` 또한 위와 같은 [cronR][821]이 있습니다. 사용하는 모양이 같으니 한번 사용해 보겠습니다. 두 가지 모두 `rstudio`를 관리자 권한으로 실행시켜줘야 합니다.

## bookdown

지금 보시는 자료를 만들때 사용한 패키지인 [bookdown][811]입니다. 들어가 보시면 R 관련한 제작자들이 직접 만든 다양한 자료들이 있습니다. 패키지를 설명하는 [책][812]이 가장 위에 있으면서 사례로 확인하실 수 있습니다. 처음부터 우수 사례를 패키지 홍보으로 활용한 매우 사례라고 생각합니다.

처음 6권과 더불어 필요에 따라 네트워크 분석을 주제로 하는 [Social Network Analysis in Education][813]도 참고하기 매우 좋은 내용 같습니다.

여기 패키지는 현재의 강의자료 소스를 활용해 작업을 완료하고, 각자 github을 통해서 호스팅을 하는 것 까지 실습하도록 하겠습니다.



[801]: https://www.rstudio.com/wp-content/uploads/2016/02/rmarkdown-cheatsheet-kr.pdf
[802]: http://rmarkdown.rstudio.com/html_document_format.html#appearance_and_style
[803]: http://commonmark.org/
[804]: https://github.com/rstudio/rmarkdown
[805]: https://www.latex-project.org/
[806]: http://t-robotics.blogspot.kr/2016/02/latex.html#.WSY5qGjyiHs
[807]: http://spec.commonmark.org/0.27/
[808]: http://rmarkdown.rstudio.com/lesson-1.html
[809]: https://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf
[810]: https://www.rstudio.com/wp-content/uploads/2016/03/rmarkdown-cheatsheet-2.0.pdf
[811]: https://bookdown.org/home/
[812]: https://bookdown.org/yihui/bookdown/
[813]: https://bookdown.org/chen/snaEd/
[814]: http://rmarkdown.rstudio.com/formats.html
[815]: https://ko.wikipedia.org/wiki/YAML
[816]: https://github.com/wch/webshot
[817]: https://www.latex-project.org/get/
[818]: https://github.com/Jaimyoung/data-science-in-korean/blob/master/r-markdown-korean.md
[819]: http://freesearch.pe.kr/archives/4034
[820]: https://github.com/bnosac/taskscheduleR
[821]: https://github.com/bnosac/cronR
