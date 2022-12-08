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

## 컨텍스트 관리자 (context manager)
컨텍스트 관리자는 파이썬이 제공하는 유용한 기능이다. 
일반적으로 리소스 관리와 관련하여 컨텍스트 관리자를 자주 볼 수 있다. 
예를 들어 파일을 열면 파일 디스크립터의 누수를 막기 위해 작업이 끝나면 적절히 닫히길 기대한다. 또는 서비스나 소켓에 대한 연결을 열었을 때도 적절하게 닫거나 임시 파일을 제거하는 등의 작업을 해야한다.

이 모든 경우에 일반적으로 할당된 모든 리소스를 해제해야 한다. 모든 것이 잘 처리되었을 경우의 해제는 쉽지만 예외가 발생하거나 오류를 처리해야 하는 경우는 어떻게 될까?

이 문제를 해결하는 가장 일반적인 방법은 `finally` 블록에 정리 코드를 넣는 것이다.

다음 두 예시를 보자.

- context_manager_example1.py

```py
fd = open(filename)
try:
    process_file(fd)
finally:
    fd.close()
```

- context_manager_example2.py

```py
with open(filename) as fd:
    process_file(fd)
```

전자는 일반적인 간단한 예제 코드이고 후자는 파이썬스러운 방법의 구현이다.

후자의 `with`  문은 컨텍스트 관리자로 진입하게 한다. 이번 예제의 경우 `open` 함수는 컨텍스트 관리자 프로토콜을 구현한다. 즉 예외가 발생한 경우에도 파일이 자동으로 닫힌다.

컨텍스트 관리자는 `__enter__`와 `__exit__` 매직 메서드로 구성된다.

with 문은 __enter__ 메서드를 호출하고 이 메서드의 반환값은 as 이후에 지정된 변수에 할당된다.

해당 블록(스코프)의 마지막줄의 실행이 끝난다면 __exit__ 컨텍스트 메서드를 호출한다.

컨텍스트 관리자 블록 내에 예외나 오류가 있는 경우에도 __exit__ 메서드가 호출되므로 안전하게 실행이 가능하다. 

### 컨텍스트 관리자 구현

다음은 파일을 여는 컨텍스트 관리자 예제 코드입니다.

- FileManager_ex.py

```py
class FileManager(object):
    def __init__(self, file_name, method):
        self.fd = open(file_name, method)

    def __enter__(self):
        return self.fd

    def __exit__(self, exc_type, exc_val, exc_tb):
        self.fd.close()
```

동작순서.
1. FileManager 클래스의 __init__()이 호출되며 open 함수로 파일을 읽어옴
2. __enter__ 메서드의 반환 값으로 파일 객체 반환되며 Context에서 opened_file라는 변수에 저장됨
3. opened_file 파일 객체의 write() 함수를 사용하여 파일을 작성함
4. Context 내의 모든 코드가 실행되면 __exit__()이 호출되며 파일 객체가 닫힘

이제 만든 클래스를 사용하여 파일을 작성해보자.

```py
from FileManager_ex import FileManager
with FileManager("test.py", "w") as opened_file:
	  opened_file.write("print('컨텍스트 관리자 클래스로 구현하여 파일 작성 성공')")
```

FileManager_ex.py와 같은 경로에 test.py가 생성되어 원하는 구문이 작성된 것을 확인할 수 있다.
