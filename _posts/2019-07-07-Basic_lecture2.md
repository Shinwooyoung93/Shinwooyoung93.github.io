---
layout: post
title:  "Basic Lecture2"
date:   2019-07-08
use_math: true
tags:
 - R
 - korean
 - Lecture
---

---
title: "Lecture2 - 프로그래밍 기초"
author: "KU, Shin wooyoung"
date: "2019-07"
output:
  html_document:
    latex_engine: xelatex
mainfont: NanumGothic
---

# 1. R의 기본기능

## 1-1. R의 기초기능(수학연산)

```{r}
1+2
```

또한 수식 내 띄어쓰기가 가능하다.

```{r}
1 + 2
```

```{r}
1 - 2
```

```{r}
1*2
```

```{r}
1/2
```

```{r}
(1+2)*3
```

R은 들여쓰기에 민감하지 않다.
```{r}
1 + 2*(3
       + 1)
```

세미콜론(;)을 이용하면 여러 개의 명령문을 한 줄에 입력할 수도 있다.
```{r}
1+2;min(1, 2, 3)
```

## 1-2. 변수의 생성 및 삭제

변수에 값을 할당하는 방법은 2가지이다.

- "="을 이용하는 방법

- "$\leftarrow$"을 이용하는 방법

할당되지 않은 변수(문자)를 실행하면 Error: object 'a' not found가 반환된다. 따라서 변수 `a`에 1을 할당해본다.
```{r, error = T}
a
a = 1
a
```

이번에는 $\leftarrow$를 이용해 `a`에 2를 할당해본다.
```{r}
a <- 2
a
```

이렇게 될 경우에는 기존에 할당했던 1이었던 `a`가 덮어쓰기에 의해 2로 재할당된다. 

다음은 변수를 삭제하는 방법이다.(`rm = remove`)
```{r}
rm(a)
```

## 1-3. 객체 명명 규칙

객체(Object)란 상수, 변수, 데이터 등 모든 대상을 칭한다. 이를 할당할 때 몇가지 규칙이 존재하는데,

1. 문자 a~z, A~Z, 숫자 0~9, 그리고 '.', '_'의 조합으로 구성한다.

2. 이름의 첫 글자로 숫자와 밑줄('_')은 사용할 수 없다.

3. 대문자와 소문자로 서로 구분된다.

4. 내장함수, 예약어는 변수명으로 사용할 수 없다.(`for`, `function` 등)
    + 사용할 수 있는 내장함수도 있지만 권장하지 않는다. 혼란을 초래할 수 있음

`ls()`는 활성화된 총 변수 목록을 의미한다.
```{r}
a <- 1;b <- 2
ls()
```

활성화된 총 변수들을 삭제하는 명령어는 다음과 같다.
```{r}
rm(list = ls())
ls()
```

## 1-4. 변수의 사용

자료를 입력할 때 기본이 되는 벡터형 자료는 `c()`함수를 이용해 입력한다.
```{r}
x <- c(1, 2, 3, 4, 5)
x
```

`c()`함수는 column의 약자로 자료를 벡터 형식으로 입력해준다.
```{r}
sum(x) # x의 총합
mean(x) # x의 평균
median(x) # x의 중앙값 
var(x) # x의 분산
```

벡터는 숫자형 뿐만 아니라 문자형과 논리형을 입력할 수 있다. 그러나 `한 벡터 내에서 여러 형태가 섞일 수 는 없다.`
```{r}
s1 <- c("a", "b", "c")
s1
s2 <- c(0, 1, 2)
s2
s3 <- c(s1, s2)
s3
mode(s3)
```

`s3`에서 2개의 벡터 `s1`과 `s2`를 하나의 벡터로 묶어주었다. 

또한 `s3`의 형태는 문자형으로 통일 되었다. 이는 문자형의 순위가 더 높아서 나타나는 현상이다.

`mode()`함수는 해당 벡터의 형태를 출력하는 함수이다.

`y`에 `x`의 자료를 복사하는 코드는 다음과 같다.
```{r}
x <- c(1, 2, 3, 4, 5)
y <- x
x
```

벡터 `y`의 1번째 값에 0을 대입해보자.
```{r}
y[1] <- 0
y
```

벡터 `y`의 5번째 값을 출력해보자.
```{r}
y[5]
```

벡터 `y`의 1번째 값을 제외하고 출력해보자.
```{r}
y[-1]
```

벡터 `y`의 1, 2, 4번째 값을 출력해보자.
```{r}
y[c(1, 2, 4)]
```

그렇다면 벡터 `y`에서 3보다 작거나 같은 값을 찾아보자.
```{r}
y
y <= 3
```

출력값은 3보다 작거나 같은 가에 대한 논리를 제공한다.

그렇다면 벡터 `y`에서 3보다 작은 값의 위치는 어디인가?
```{r}
which(y <= 3)
```

1, 2, 3번째가 3보다 작은 위치에 있다는 것을 알 수 있다. 

이번에는 가장 작은 값의 위치를 알아보자.
```{r}
which.min(y)
```

1번째가 가장 작은 위치에 있다는 것을 알 수 있다.

벡터 `y`에서 3보다 작은 값의 갯수는
```{r}
sum(y <= 3)
```

벡터끼리의 연산을 알아보자.
```{r}
x <- c(1, 3, 5)
y <- 4:6 # equal to y <- c(4, 5, 6)
z <- c(1, 2)
x + z
```

Warning은 나오지만 Error가 아니므로 코드는 실행이 된다. 

`x`와 `z`의 벡터크기가 같지 않으므로 연산이 되지 않을 것 같지만 R에서는 벡터의 크기가 큰 `x`에 `z`를 맞춰준다.

즉 `(1, 3, 5) + (1, 2, 1)`로 연산이 된다.
```{r}
x * y
```

각자 원소들끼리 곱을 해준다.
```{r}
2*x
sum(x*y)
```

벡터를 열로 결합하고 싶을 때는 `cbind()`함수를 사용한다.
```{r}
?cbind # equal to help(cbind)
```
```{r, echo=FALSE, out.width = '60%', fig.align='center'}
knitr::include_graphics("1.png")
```

```{r}
z <- cbind(x, y)
z
w <- rbind(x, y)
w
```

이며 `w`에서 2행 3열(2, 3)의 원소를 알고 싶을 때는 다음의 코드를 사용한다.
```{r}
w[2, 3]
```

## 1-5. R의 수리연산

|Operator|Description|
|:---:|:---:|
|+|addition|
|-|subtraction|
|*|multiplication|
|/|division|
|^ or **|exponentiation|
|x %% y|modulus (x mod y) 5%%2 is 1|
|x %/% y|integer division 5%/%2 is 2|
|x %*% y|vector(or matrix) multiplication|

## 1-6. R의 논리연산

|Operator|Description|
|:---:|:---:|
|<|less than|
|<=|less than or equal to|
|>|greater than|
|>=|greater than or equal to|
|==|exactly equal to|
|!=|not equal to|
|!x|Not x|
|x$|$y|x OR y|
|x&y|x AND y|
|isTrue(x)|test if X is TRUE|

간단한 예시를 살펴보자.
```{r}
x <- 1:6 # equal to c(1,2,3,4,5,6)
x == 2
x != 2
(x>=3) & (x<6)
(x<=5) & (x==6)
(x<=5) | (x==6)
```

# 2. Question

## 2-1. Question

1부터 1000까지의 수에서 짝수만을 계산하여 평균을 구하시오.
```{r, echo = F}
x <- 1:1000
y <- x[x%%2==0]
mean(y)
```

## 2-2. Question

아래의 코드를 입력한 후, 홀수 번째에 해당하는 알파벳을 추출해 `adj.alphabet`이라는 변수에 할당하시오.
```{r}
alphabet <- LETTERS
alphabet
```

```{r, echo = F}
n <- length(alphabet)
index <- (1:n)%%2 == 0
adj.alphabet <- alphabet[index]
adj.alphabet
```