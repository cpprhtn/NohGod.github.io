---
title: Do it 자바스크립트 4장 제어문
author: 조준형
date: 작성일 2022-11-26 20:00:00 +09
categories: [스터디, JavaScript]
tags: [JavaScript, 컴퓨터공학, 프론트엔드]
---




# Do it 자바스크립트 4번째

## 4장 제어문

### 4.1 if문

---

()안의 조건이 true이면 {}안의 자바스크립트 소스를 실행하고 false면 {}안의 자바스크립트를 무시

```jsx
if(true) {
	 document.write("if문의 조건을 만족하여 이 문장이 실행되었습니다.");
}
```

```jsx
if(false) {
	 document.write("if문의 조건을 만족하여 이 문장이 실행되었습니다.");
}
```

![if문 true_false.png](/assets/img/JavaScript-4/if문true_false.png)

### 4.2 if ~ else 문

---

()안의 조건이 true이면 if문을 실행하고 false면 else문을 실행

```jsx
var number = prompt("숫자를 입력하세요.");
if(number < 0) {
	 alert("0 이상의 수를 입력하세요.");
}
else {
	 document.write("입력한 숫자: " + number);
}
```

![ifelse문_1.png](/assets/img/JavaScript-4/ifelse문_1.png)

![ifelse문_2.png](/assets/img/JavaScript-4/ifelse문_2.png)

![ifelse문_3.png](/assets/img/JavaScript-4/ifelse문_3.png)

![ifelse문_4.png](/assets/img/JavaScript-4/ifelse문_4.png)

![ifelse문_5.png](/assets/img/JavaScript-4/ifelse문_5.png)

### 4.3 조건 연산자 - ?와:

---

조건이 하나이고 실행할 명령도 하나라면 if~else문보다 조건연산자를 이용하는것이 더 간단

- 조건 연산자 사용 방법
    
    ? 왼쪽에 조건을 씀
    
    : 왼쪽에 조건이 true일때 실행할 명령을 씀
    
    : 오른쪽에 조건이 false일때 실행할 명령을 씀
    

```jsx
var score = 75;
(score >= 60) ? alert("통과") : alert("실패");
```

![조건연산자.png](/assets/img/JavaScript-4/조건연산자.png)

### 4.4 truthy 값과 falsey 값

---

논리형 자료 값은 true와 fasle 뿐이지만 일반 값 중에서도 ‘true로 인정할 수 있는 값’ 과 ‘false로 인정할 수 있는 값’이 있음

이것을 ‘truthy하다’ , ‘falsey하다’ 라고 표현함

- 자바스크립트에서 falsey하게 인정하는 값
    
    0                     //숫자
    
    “”                    //빈 문자열
    
    NaN               // 숫자가 아님( Not a Number)
    
    undefined
    
    null
    

falsey하게 인정하는 값을 제외한 나머지 값은 자바스크립트에서 truthy값이 됨

```jsx
var input = prompt("이름을 입력하세요.");
if(input) {
	 alert("이름을 입력했습니다 : " + input);
}
else {
	 alert("이름을 입력하지 않았습니다.");
}
```

이름을 입력했을 때

![truthy값과falsey값_1.png](/assets/img/JavaScript-4/truthy값과falsey값_1.png)

![truthy값과falsey값_2.png](/assets/img/JavaScript-4/truthy값과falsey값_2.png)

아무것도 입력하지 않았을 때

![truthy값과falsey값_3.png](/assets/img/JavaScript-4/truthy값과falsey값_3.png)

### Do it 실습 3의 배수 검사기 만들기

---

```jsx
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>3의 배수인지 확인</title>
	<link rel="stylesheet" href="css/multi3.css">
</head>
<body>
	<div id="result"></div>
	<script>
		var userNumber = prompt("숫자를 입력하세요. ");
		var displayArea = document.querySelector('#reslut');

		if(userNumber != null) {			//[확인]을 눌렀을 때 실행할 명령
			if(userNumber % 3 == 0) {		// 3의 배수일 때 실행할 명령
				displayArea.innerHTML = userNumber + "은 3의 배수입니다.";
			}
			else {							// 3의 배수가 아닐 때 실행할 명령
				displayArea.innerHTML = userNumber + "은 3의 배수가 아닙니다.";
			}
		}
		else {
			alert("입력이 취소되었습니다.");  //[취소]를 눌렀을 때 실행할 명령
		}
	</script>
</body>
</html>
```

- 실행 결과

![doit실습3의배수_1.png](/assets/img/JavaScript-4/doit실습3의배수_1.png)

- [취소]를 눌렀을 때

![doit실습3의배수_2.png](/assets/img/JavaScript-4/doit실습3의배수_2.png)

- 3의 배수가 아닌 숫자를 입력했을 때

![doit실습3의배수_3.png](/assets/img/JavaScript-4/doit실습3의배수_3.png)

![doit실습3의배수_4.png](/assets/img/JavaScript-4/doit실습3의배수_4.png)

- 3의 배수인 숫자를 입력했을 때

![doit실습3의배수_5.png](/assets/img/JavaScript-4/doit실습3의배수_5.png)

![doit실습3의배수_6.png](/assets/img/JavaScript-4/doit실습3의배수_6.png)

### 4.5 switch문

---

여러 가지 조건과 입력값을 비교해야하는 경우 if문과 esle문을 여러번 사용하는것 보단 switch문을 사용하는 것이 더 편리함

- switch문 사용 방법
    
    switch 예약어 오른쪽에 괄호와 함께 값을 확인할 변수 지정
    
    여러 가지 조건 값은 case문 다음에  :  을 붙여 지정, 해당 값일 때 실행할 명령도 : 다음에 나열
    
    break문을 사용해서 명령을 실행한 다음 완전히 switch문을 빠져나오도록 작성
    
    default는 사용자가 입력한 값이 case문과 전부 일치하지 않을 때 실행할 명령
    

```jsx
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>세션 선택</title>
	<link rel="stylesheet" href="css/switch.css">
</head>
<body>
	<script>
		var session = prompt("관심 세션을 선택해 주세요. 1-마케팅, 2-개발, 3-디자인", "1");
		
		switch(session) {
			case "1" : document.write("<p>마케팅 세션은 <strong>201호</strong>에서 진행합니다.</p>");
				break;
			case "2" : document.write("<p>마케팅 세션은 <strong>203호</strong>에서 진행합니다.</p>");
				break;
			case "3" : document.write("<p>마케팅 세션은 <strong>205호</strong>에서 진행합니다.</p>");
				break;
		default : alert("잘못 입력했습니다.");
		}
	</script>
</body>
</html>
```

case “1” 이 실행

![switch문_1.png](/assets/img/JavaScript-4/switch문_1.png)

![switch문_2.png](/assets/img/JavaScript-4/switch문_2.png)

case “2” 가 실행

![switch문_3.png](/assets/img/JavaScript-4/switch문_3.png)

![switch문_4.png](/assets/img/JavaScript-4/switch문_4.png)

case “3” 이 실행

![switch문_5.png](/assets/img/JavaScript-4/switch문_5.png)

![switch문_6.png](/assets/img/JavaScript-4/switch문_6.png)

default 가 실행

![switch문_7.png](/assets/img/JavaScript-4/switch문_7.png)

![switch문_8.png](/assets/img/JavaScript-4/switch문_8.png)

### 4.6 for문

---

어떤 동작을 여러번 실행할 때 사용

- for문 사용 방법
    
    카운터 변수 선언
    
    조건식 입력
    
    반복 실행할 소스
    
    카운터 변수 조절
    

<aside>
💡 카운터 변수는 for문을 실행할 때 반복 횟수의 기준이 되는 변수

</aside>

```jsx
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>중첩된 for 문</title>
	<link rel="stylesheet" href="css/for.css">
</head>
<body>
	<script>
		var sum = 0;

		for(var i = 0; i < 6; i++) {
			sum += i;
		}
		document.write("1부터 5까지 더하면 " + sum);
	</script>
</body>
</html>
```

![for문.png](/assets/img/JavaScript-4/for문.png)

### 4.7 중첩 for문

---

```jsx
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>중첩된 for 문</title>
	<link rel="stylesheet" href="css/for.css">
</head>
<body>
	<script>
		for(var i = 0; i < 30; i++) {
			document.write('*');
		}
	</script>
</body>
</html>
```

![중첩for문_1.png](/assets/img/JavaScript-4/중첩for문_1.png)

5줄로 만들고 싶을 때

```jsx
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>중첩된 for 문</title>
	<link rel="stylesheet" href="css/for.css">
</head>
<body>
	<script>
		for(var i = 0; i < 30; i++) {
			document.write('*');
		}
		document.write("<br>");
		for(var i = 0; i < 30; i++) {
			document.write('*');
		}
		document.write("<br>");
		for(var i = 0; i < 30; i++) {
			document.write('*');
		}
		document.write("<br>");
		for(var i = 0; i < 30; i++) {
			document.write('*');
		}
		document.write("<br>");
		for(var i = 0; i < 30; i++) {
			document.write('*');
		}
	</script>
</body>
</html>
```

![중첩for문_2.png](/assets/img/JavaScript-4/중첩for문_2.png)

중첩 for문을 이용했을 때

```jsx
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>중첩된 for 문</title>
	<link rel="stylesheet" href="css/for.css">
</head>
<body>
	<script>
		for(var k = 0; k < 5; k++) {
			for(var i = 0; i < 30; i++) {
				document.write('*');
			}
			document.write("<br>");
		}

	</script>
</body>
</html>
```

![중첩for문_3.png](/assets/img/JavaScript-4/중첩for문_3.png)

위의 소스가 실행되는 순서

1. 바깥쪽 for문을 실행 (k =0)
2. 안쪽 for문을 실행해 30번 반복하고 빠져나옴
3. <br>태그를 추가하여 줄을 바꿈
4. 바깥쪽 for문의 조건식이 false가 될 때까지 반복

### Do it 실습 구구단 만들기

---

```jsx
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>구구단 - for문</title>
	<link rel="stylesheet" href="css/gugudan.css">
</head>
<body>
	<h1>구구단</h1>
	<script>
		for(var i = 2; i <= 9; i++) {
			document.write("<div>");
			document.write("<h3>" + i + "단</h3>");
			for(var j = 1; j <= 9; j++) {
				document.write(i + "X" + j + " = " + i * j + "<br>");
			}
			document.write("</div>");
		}
	</script>
</body>
</html>
```

- 실행결과

![doit실습구구단.png](/assets/img/JavaScript-4/doit실습구구단.png)

### 4.8 while문과 do~while문

---

while 문과 do~while 문은 특정 조건을 만족하는 동안에만 명령을 반복

- while 문 동작 순서
    1. 조건식 검사
    2. 중괄호 안의 자바스크립트 소스 실행

```jsx
var i = 0;
while (i < 10) {
    document.write('반복 조건이 true이면 반복합니다. <br>');
		i += 1;
}
```

![while문.png](/assets/img/JavaScript-4/while문.png)

do~while 문은 while 문과 달리 조건이 맨 뒤에 붙음

일단 문장을 한번 실행한 후 조건을 확인함

```jsx
var i = 0;
do {
	 document.write('반복 조건이 true이면 반복합니다. <br>'); //조건 실행
	 i += 1;
} while (i < 10);   //조건이 false가 되면 반복 종료
```

![dowhile문.png](/assets/img/JavaScript-4/dowhile문.png)

### Do it 실습 팩토리얼 계산기

---

```jsx
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>팩토리얼 계산하기</title>
	<link rel="stylesheet" href="css/factorial.css">
</head>
<body>
	<script>
		var n = prompt("숫자를 입력하세요.");	//몇까지 곱할 것인지를 프롬포트 창으로 입력받아 변수에 저장
		var nFact = 1;	//팩토리얼 계산 결과값을 저장할 변수 1을 기본값으로 지정
		var i = 2;	//반복문에 사용할 카운터 변수  1! = 1 이기 때문에 i = 2부터 시작

		while(i <= n) {	//i = n 까지 반복
			nFact *= i;	//nFact = nFact * i
			i++;
		}

		document.write(n + "!= " + nFact);
	</script>
</body>
</html>
```

- 실행결과

![doit실습팩토리얼_1.png](/assets/img/JavaScript-4/doit실습팩토리얼_1.png)

![doit실습팩토리얼_2.png](/assets/img/JavaScript-4/doit실습팩토리얼_2.png)

![doit실습팩토리얼_3.png](/assets/img/JavaScript-4/doit실습팩토리얼_3.png)

### 4.9 break 문, continue 문

---

- break 문
    
    반복문의 흐름에서 바로 빠져나올 때 사용
    

```jsx
for (var i = 0; i < 10; i++) {
	 document.write("*");
	 break;  //이 지점에 오면 바로 반복문 종료
}
```

![break문.png](/assets/img/JavaScript-4/break문.png)

- continue 문
    
    주어진 조건에 맞는 값을 만났을 때 실행하던 반복 문장을 건너뛰고 반복문의 맨 앞으로 되돌아가고 다시 반복 시작
    

```jsx
for (var i = 0; i < 10; i++) {
	 document.write("*");
	 continue;
	 document.write("continue 문 때문에 이문장은 건너뜁니다.");
}
```

![continue문.png](/assets/img/JavaScript-4/continue문.png)

### Do it 실습 짝수 더하기

---

```jsx
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>짝수 더하기</title>
	<link rel="stylesheet" href="css/even.css">
</head>
<body>
	<h1>짝수끼리 더하기</h1>
	<script>
		var n = 10;
		var sum = 0;

		for(var i = 1; i <= n; i++) {	// i <= 10까지 반복
			if(i % 2 == 1) {	// i가 홀수일 경우 실행
				continue;
			}
			sum += i;

			document.write(i + " ------ " + sum + "<br>");
		}
	</script>
</body>
</html>
```

- 실행결과

![doit실습짝수끼리더하기.png](/assets/img/JavaScript-4/doit실습짝수끼리더하기.png)