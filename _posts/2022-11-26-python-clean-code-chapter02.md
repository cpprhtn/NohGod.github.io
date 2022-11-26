---
title: 파이썬 클린코드 Chapter02
author: 이준원
date: 2022-11-26 12:00:00 +0900
categories: [스터디, Python]
tags: [Python, 클린코드, 컴퓨터공학]
---

# Chapter2 파이썬스러운 코드 (pythonic code)

## 인덱스와 슬라이스
다른 언어와 마찬가지로 파이썬의 일부 데이터 구조나 타입은 자신이 가지고 있는 요소에 인덱스를 통해 접근하는 것을 지원한다.  
일반적인 프로그래밍 언어와 같이 첫 번째 요소의 인덱스는 0부터 시작한다.  
그러나 파이썬은 다른 언어와 색다른 방법으로 접근하는 것을 지원한다.

파이썬에서는 음수 인덱스를 사용하여 끝에서부터 접근이 가능하다.  
다음과 같이 사용이 가능하다.

```py
> my_numbers = (4, 5, 3, 9)
> my_numbers[-1]
9
> my_numbers[-3]
5
```

하나의 요소를 얻는 것 외에도 다음 명령과 같이 `slice`를 사용하여 특정 구간의 요소를 구할 수도 있다.

```py
> my_numbers = (1, 1, 2, 3, 5, 8, 13, 21)
> my_numbers[2:5]
(2, 3, 5)
```

시작, 끝 또는 간격 파라미터 중 하나를 제외할 수 있으며 이 경우 다음에 보이는 것처럼 시퀀스의 처음 또는 끝에서부터 동작한다.

```py
> my_numbers[:3]
(1, 1, 2)
> my_numbers[3:]
(3, 5, 8, 13, 21)
> my_numbers[::]
(1, 1, 2, 3, 5, 8, 13, 21)
> my_numbers[1:7:2]
(1, 3, 8) 
```

위 모든 예제는 실제로는 slice 함수에 파라미터를 전달하는 것과 같다.  
slice 함수는 파이썬의 내장 객체이므로 다음과 같이 직접 호출할 수도 있다.  
slice의 (시작, 중지, 간격) 중 지정하지 않은 파라미터는 None으로 간주한다.  

```py
> interval = slice(1, 7, 2)
> my_numbers[interval]
(1, 3, 8)

> interval = slice(None, 3)
> my_numbers[interval] == my_numbers[:3]
True
```

### 자체 시퀀스 생성
방금 설명한 기능은 `__getitem__` 이라는 매직 메서드이다.  
이것은 myobject[key]와 같은 형태를 사용하거나 슬라이싱 기능 등을 사용할 수 있게 하는 시퀀스 객체의 예이다.

다음은 사용자 정의 클래스에 __getitem__을 구현하는 예시이다.

- items.py

```py
class Items:
	def __init__(self, *values):
		self._values = values

	def __len__(self):
		return len(self._values)

	def __getitem__(self, item):
		return self._values.__getitem__(item)
```

- 사용 예시

```py
> from items import Items
> A = Items("Lee", "Junwon", "Cpprhtn", 2002 , True)
> len(A)
5
> A[:]
('Lee', 'Junwon', 'Cpprhtn', 2002, True)
> A[:2]
('Lee', 'Junwon')
> A[-1]
True
> A[::2]
('Lee', 'Cpprhtn', True)
> A[2][:3]
Cpp
```