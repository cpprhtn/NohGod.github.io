---
title: 파이썬 클린코드 Chapter01
author: 이준원
date: 2022-11-26 00:00:00 +0900
categories: [스터디, Python]
tags: [Python, 클린코드, 컴퓨터공학]
---

# Chapter1 코드 포매팅과 도구

## 클린 코드의 의미
클린 코드에 대한 유일하고 엄격한 정의는 없다.  
클린 코드인지 아닌지는 다른 엔지니어가 코드를 읽고 유지 관리할 수 있는지 여부에 달려 있다.  
이 책을 통해 파이썬의 주요 개념을 이해한 다음 좋은 코드와 나쁜 코드의 차이점을 확인하고, 
훌륭한 코드와 좋은 아키텍처의 특징을 식별하여 자신만의 정의를 가져가자.

## 클린 코드의 중요성
클린 코드는 유지보수성 향상, 기술 부채의 감소, 애자일 개발을 통한 효과적인 작업 진행, 성공적인 프로젝트 관리로 이어진다.

### 클린 코드를 지킬 필요가 없는 경우
- 해커톤 참여
- 일회성 작업을 위한 간단한 스크립트를 작성하는 경우
- 프로그래밍 경진 대회 참여
- 기존에 없던 개념을 검증하기 위해 개발하는 경우
- (나중에 버려질 것이 확실하다고 생각되는) 프로토타입을 개발할 때
- 앞으로 버려질 것이 확실한 레거시 프로젝트에 짧은 시간 동안만 작업을 하는 경우


## 문서화(Documentation)
### 코드 주석(code comments)
가능한 한 적은 주석을 갖는 것을 목표로 해야 한다. 좋은 코드는 코드 자체가 문서화되어 있기 때문이다.  
다시 말하면 올바른 추상화를 했고, 명확하게 이름을 지정했다면 주석이 필요하지 않아야한다.  
(주석을 작성하기 전에 새로운 함수를 추가하거나 보다 나은 변수명을 사용하는 것과 같은 방법으로 개선할 수 있는지 고민해보라.)

어떤 경우에는 주석을 추가하는 것을 피할 수 없는 경우도 있다.  
예를 들어, 외부 함수의 문제를 피하기 위해 특정한 파라미터를 넘겨야 하는 경우와 같다.  
이러한 경우는 가능한 간결하게 문제가 무엇인지 설명하고 어떻게 해결해야 하는지 설명해야 한다.

주석 처리된 코드는 대부분의 경우 혼란을 가져온다. 필요한 경우가 아니라면 주석 처리된 코드를 남겨둘 필요는 없다.

### Docstring
Docstring은 소스 코드에 포함된 문서라고 말할 수 있다.  
Docstring은 모듈, 클래스, 메서드 또는 함수에 대해 문서를 제공하기 위한 것이다.   
내가 작성한 컴포넌트를 다른 엔지니어가 사용하려고 할 때 docstring을 보고 동작방식과 입출력 정보 등을 확인할 수 있어야 한다.

- example.py

```py
class CustomClass:
"""
클래스의 문서화 내용을 입력합니다.    
"""

    def custom_function(param):
        """
        함수의 문서화 내용을 입력합니다.
        """
        # ... 코드  ...

```

이를 이용하여 다음과 같은 문서를 만들 수 있다.

- words.py

```py
"""
    URL로부터 파일을 가져와 단어를 print 함.
Usage:

    python words.py <URL>
"""

from urllib.request import urlopen

import sys


def fetch_words(url):
    """
    url주소에서 파일을 가져와 단어 리스트를 반환합니다.
    :param url: 불러올 url
    :return:
    """
    with urlopen(url) as story:
        story_words = []
        for line in story:
            line_words = line.decode('utf-8').split()
            for word in line_words:
                story_words.append(word)
    return story_words


def print_items(items):
    """
    items를 print
    :param items: 
    :return: 
    """
    for item in items:
        print(item)


def main(url):
    '''
    url을 받아 단어를 print 함
    :param url: url
    :return:
    '''
    words = fetch_words(url)
    print_items(words)


if __name__ == '__main__':
    main(sys.argv[1])

```

- 모듈 불러오기

```py
> import words
> help(words)

```

- 출력결과

```py
Help on module words:

NAME
    words

DESCRIPTION
    URL로부터 파일을 가져와 단어를 print 함.
    Usage:
    
        python words.py <URL>

FUNCTIONS
    fetch_words(url)
        url주소에서 파일을 가져와 단어 리스트를 반환합니다.
        :param url: 불러올 url
        :return:
    
    main(url)
        url을 받아 단어를 print 함
        :param url: url
        :return:
    
    print_items(items)
        items를 print
        :param items: 
        :return:
        
FILE
    c:\users\cpprh\desktop\words.py

```


## 어노테이션(Annotation)
코드 사용자에게 함수 인자로 어떤 값이 와야하는지 힌트를 주는 역할을 한다.

- annotations.py

```py
@dataclass
class Point:
    lat: float
    long: float


def locate(latitude: float, longitude: float) -> Point:
    """맵에서 좌표에 해당하는 객체를 검색"""
    return Point(latitude, longitude)
```

파이썬이 타입을 검사하거나 강제하지는 않는다. 하지만 어노테이션을 사용하면 가독성을 가지는 코드를 작성할 수 있다.

- bad_case.py

```py
def launch_task(delay_in_seconds):
    ...
```
여기에서 delay_in_seconds 파라미터는 많은 정보를 담고 있는 것 같아보이지만 사실은 충분한 정보를 제공하지 못하고 있다.

허용 가능한 지연 시간은 몇 초일까? 분수를 입력해도 되는 걸까?와 같은 궁금증을 해결해줄 수 없다.

- good_case.py

```py
Seconds = float
def launch_task(delay: Seconds):
    ...
```

다음 코드는 코드 스스로가 자신의 기능에 대해 말을 하고 있다. 
뿐만 아니라 Seconds 어노테이션을 사용하여 시간을 어떻게 해석할지에 대해 작은 추상화를 했다고 볼 수도 있다.
또한 나중에 입력값을 변경하기로 했다면 한 곳에서만 내용을 변경하면 된다.


```py
def process_clients(clients: list):
    ...
```

```py
def process_clients(clients: list[tuple[int, str]]):
    ...
```

```py
Client = Tuple[int, str]
def process_clients(clients: list[Client]):
    ...
```
다음 코드는 클라이언트 배열에 대해서 어떤 작업을 수행하는 함수를 표현한 것이다.
이렇게 하는 근본 취지는 유의미한 문법 구조를 통해 코드의 의미나 의도를 더욱 쉽게 이해할 수 있도록 하자는 것이다.

```py
class Point:
    def __init__(self, lat, long):
        self.lat = lat
        self.long = long
```

```py
@dataclass
class Point:
    lat: float
    long: float
```
@dataclass 데코레이터를 사용하면 별도의 __init__ 메서드에서 변수를 선언하고 할당하는 작업을 하지 않아도 바로 인스턴스 속성으로 인식한다.

이러한 docstring을 사용했을 때의 이슈는 코드가 좀 더 커지게 되고, 실제 효과적인 문서가 되려면 보다 상세한 정보가 필요하다.

이상으로 Chapter1 코드 포매팅과 도구에 대한 설명을 마친다.
