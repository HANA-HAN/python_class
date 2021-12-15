# 11. Module

## 11.1 모듈
모듈(Module)은 파이썬 코드를 논리적으로 묶어서 관리하고 사용할 수 있도록 하는 것으로, 보통 하나의 파이썬 .py 파일이 하나의 모듈이 된다. 모듈 안에는 함수, 클래스, 혹은 변수들이 정의될 수 있으며, 실행 코드를 포함할 수도 있다.

파이썬은 기본적으로 상당히 많은 표준 라이브러리 모듈들을 제공하고 있으며, 3rd Party에서도 많은 파이쎤 모듈들을 제공하고 있다. 이러한 모듈들을 사용하기 위해서는 모듈을 import하여 사용하면 되는데, import 문은 다음과 같이 하나 혹은 복수의 모듈을 불러들일 수 있다.

```
import 모듈1[, 모듈2[,... 모듈N]
```

예를 들어, 아래 예제는 표준 라이브러리 중 수학과 관련된 함수들을 모아 놓은 "math" 모듈을 import 하여 그 모듈 안에 있는 factorial() 함수를 사용하는 예이다.

```python
import math
n = math.factorial(5)
```

하나의 모듈 안에는 여러 함수들이 존재할 수 있는데, 이 중 하나의 함수만을 불러 사용하기 위해서는 아래와 같이 "from 모듈명 import 함수명"이라는 표현을 사용할 수 있다. 이렇게 from...import... 방식으로 import 된 함수는 호출시 "모듈명.함수명"이 아니라 직접 "함수명"만을 사용한다.

```python
# factorial 함수만 import
from math import factorial  
 
n = factorial(5) / factorial(3) 
```

하나의 모듈 안에는 있는 여러 함수를 사용하기 위해 from... import (함수1, 함수2) 와 같이 import 뒤에 사용할 함수를 나열할 수도 있다. 또한, 모든 함수를 불러 사용하기 위해서는 "from 모듈명 import *" 와 같이 asterisk(*)를 사용할 수 있다. 이렇게 from...import... 방식으로 import 된 함수는 호출시 모듈명 없이 직접 함수명을 사용한다.

```python
# 여러 함수를 import
from math import (factorial,acos)
n = factorial(3) + acos(1)
 
# 모든 함수를 import
from math import *
n = sqrt(5) + fabs(-12.5) 
```

함수의 이름이 길거나 어떤 필요에 의해 함수의 이름에 Alias를 주고 싶은 경우가 있는데, 이 때는 아래와 같이 "함수명 as Alias" 와 같은 표현을 사용할 수 있다.

```python
# factorial() 함수를 f()로 사용 가능
from math import factorial as f
n = f(5) / f(3)
```

## 11.2 모듈의 위치
파이썬에서 모듈을 import 하면 그 모듈을 찾기 위해 다음과 같은 경로를 순서대로 검색한다.

1. 현재 디렉토리
1. 환경변수 PYTHONPATH에 지정된 경로
1. Python이 설치된 경로 및 그 밑의 라이브러리 경로

이러한 경로들은 모두 취합되어 시스템 경로인 sys.path에 리스트 형태로 저장된다. 따라서, 모듈이 검색되는 검색 경로는 sys.path를 체크하면 쉽게 알 수 있다. 모듈을 import 하면 sys.path에 있는 경로 순서대로 모듈을 찾아 import하다가 만약 끝까지 찾지 못하면 에러가 발생된다.
sys.path를 사용하기 위해서는 sys라는 시스템 모듈을 import 해야 하며, sys.path는 임의로 수정할 수도 있다. 예를 들어, 기존 sys.path에 새 경로를 추가(append)하면, 추가된 경로도 이후 모듈 검색 경로에 포함된다

아래는 sys.path를 출력해 본 예인데, sys.path[0]의 값은 빈 문자열(empty string)로 이는 현재 디렉토리를 가리킨다. 즉, 먼저 현재 디렉토리부터 찾는다는 뜻이다. 마지막 라인은 sys.path.append()를 사용하여 새 경로를 추가하는 예를 든 것이다.

```python
import sys
sys.path # 현재 검색경로를 표시함
# 출력: ['', 'C:\\Python25\\Lib\\idlelib', 'C:\\Python35\\python35.zip', 'C:\\Python35\\DLLs', 'C:\\Python35\\lib', 'C:\\Python35', 'C:\\Python35\\lib\\site-packages']
sys. path[0] # 첫번째는 빈 문자열로 현재 디렉토리를 가리킴
sys.path.append('C:\PySrc') #새 폴더를 검색경로에 추가함
```

## 11.3 모듈의 작성
프로그램을 모듈로 나누어 코딩하고 관리하는 것은 종종 많은 잇점이 있다. 사용자 함수 혹은 클래스를 묶어 모듈화하고, 이를 불러 사용하는 방법을 간략히 살펴보자. 우선 아래 두 개의 함수(add와 substract)를 mylib.py 라는 모듈에 저장한다.

```python
# mylib.py
def add(a, b):
    return a + b
 
def substract(a, b):
    return a - b
```

모듈 mylib.py가 있는 디렉토리에서 그 모듈을 import 한 후, mylib의 함수들을 사용한다.

```python
# exec.py
from mylib import *
 
i = add(10,20)
i = substract(20,5)
```

파이썬 모듈 .py 파일은 import 하여 사용할 수 있을 뿐만 아니라, 해당 모듈 파일 안에 있는 스크립트 전체를 바로 실행할 수도 있다. 파이썬에서 하나의 모듈을 import 하여 사용할 때와 스크립트 전체를 실행할 때를 동시에 지원하기 위하여 흔히 관행적으로 모듈 안에서 __name__ 을 체크하곤 한다. 파이썬에서 모듈을 import해서 사용할 경우 그 모듈 안의 __name__ 은 해당 모듈의 이름이 되며, 모듈을 스크립트로 실행할 경우 그 모듈 안의 __name__ 은 "__main__" 이 된다. 예를 들어, run.py이라는 모듈을 import 하여 사용할 경우 __name__ 은 run.py가 되며, "python3.5 run.py"와 같이 인터프리터로 스크립트를 바로 실행할 때 __name__ 은 __main__ 이 된다.

```python
# run.py
import sys
def openurl(url):
    #..본문생략..
    print(url)
 
if __name__ == '__main__':
    openurl(sys.argv[1]) 
```

위와 같은 run.py 모듈을 아래와 같이 스크립트로 실행할 때 "if __name__ ..." 조건문은 참이 되어 openurl(sys.argv[1]) 가 실행된다. 여기서 참고로 sys.argv는 Command Line 아규먼트들을 갖는 리스트로서 아래 예제에서 argv[0]은 run.py, argv[1]은 google.com이 된다.

```
$ python3.5 run.py google.com
google.com
```

하지만 아래와 같이 모듈을 import하여 사용할 때는 "if __name__ ..." 문이 거짓이 되어 openurl() 함수가 바로 실행되지 않고, 그 함수 정의만 import 된다. 따라서 이 경우 사용자는 명시적으로 openurl() 함수를 호출하여 사용해야 한다.

```
$ python3.5 
>>> from run import *
>>> openurl('google.com')
```
