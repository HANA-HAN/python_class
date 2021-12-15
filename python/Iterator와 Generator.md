# 17. Iterator와 Generator

## 17.1 Iterator
리스트, Set, Dictionary와 같은 컬렉션이나 문자열과 같은 문자 Sequence 등은 for 문을 써서 하나씩 데이타를 처리할 수 있는데, 이렇게 하나 하나 처리할 수 있는 컬렉션이나 Sequence 들을 Iterable 객체(Iterable Object)라 부른다.

```python
# 리스트 Iterable
for n in [1,2,3,4,5]:
    print(n)
 
# 문자열 Iterable
for c in "Hello World":
    print(c)
```

내장 함수 iter()는 "iter(Iterable객체)" 와 같이 사용하여 그 Iterable 객체의 iterator를 리턴한다. Iterable 객체에서 실제 Iteration을 실행하는 것은 iterator로서, iterator는 next 메서드를 사용하여 다음 요소(element)를 가져온다. 만약 더이상 next 요소가 없으면 StopIteration Exception을 발생시킨다.

Iterator의 next 메서드로서 Python 2에서는 "iterator객체.next()" 를 사용하고, Python 3에서는 "iterator객체.__next__()" 메서드를 사용한다. 또한, 버전에 관계없이 사용할 수 있는 방식으로 내장 함수 "next(iterator객체)" 를 사용할 수 있다. 아래는 한 리스트에 대해 list iterator를 구한 후, next() 함수를 계속 호출해 본 예이다.

![Iterator](http://pythonstudy.xyz/images/basics/iter-next.png)

어떤 클래스를 Iterable 하게 하려면, 그 클래스의 iterator를 리턴하는 __iter__() 메서드를 작성해야 한다. 이 __iter__() 메서드가 리턴하는 iterator는 동일한 클래스 객체가 될 수도 있고, 별도로 작성된 iterator 클래스의 객체가 될 수도 있다. 어떠한 경우든 Iterator가 되는 클래스는 __next()__ 메서드 (Python 2 인 경우 next() 메서드) 를 구현해야 한다. 실제 for 루프에 Iterable Object를 사용하면, 해당 Iterable의 __iter__() 메서드를 호출하여 iterator를 가져온 후 그 iterator의 next() 메서드를 호출하여 루프를 돌게 된다.

아래 예제는 간단한 Iterator를 예시한 것으로 __iter__() 메서드에서 self 를 리턴함으로써 Iterable과 동일한 클래스에 Iterator를 구현했음을 표시하였고, 그 클래스 안에 Iterator로서 필요한 __next__() 메서드 (Python 3)를 구현하였다.

```python
class MyCollection:
    def __init__(self):
        self.size = 10
        self.data = list(range(self.size))
 
    def __iter__(self):
        self.index = 0
        return self
 
    def __next__(self):
        if self.index >= self.size:
            raise StopIteration
 
        n = self.data[self.index]
        self.index += 1
        return n
 
 
coll = MyCollection()
for x in coll:
    print(x)
```

## 17.2 Generator
Generator는 Iterator의 특수한 한 형태이다.
Generator 함수(Generator function)는 함수 안에 yield 를 사용하여 데이타를 하나씩 리턴하는 함수이다. Generator 함수가 처음 호출되면, 그 함수 실행 중 처음으로 만나는 yield 에서 값을 리턴한다. Generator 함수가 다시 호출되면, 직전에 실행되었던 yield 문 다음부터 다음 yield 문을 만날 때까지 문장들을 실행하게 된다. 이러한 Generator 함수를 변수에 할당하면 그 변수는 generator 클래스 객체가 된다.

아래 예제는 간단한 Generator 함수와 그 호출 사례를 보인 것이다. 여기서 gen() 함수는 Generator 함수로서 3개의 yield 문을 가지고 있다. 따라서 한번 호출시마다 각 yield 문에서 실행을 중지하고 값을 리턴하게 된다.

```python
# Generator 함수
def gen():
    yield 1
    yield 2
    yield 3
 
# Generator 객체
g = gen()
print(type(g))  # <class 'generator'>
 
# next() 함수 사용
n = next(g); print(n)  # 1
n = next(g); print(n)  # 2
n = next(g); print(n)  # 3
 
# for 루프 사용 가능
for x in gen():
    print(x)
```

위의 예에서 g = gen() 문은 Generator 함수를 변수 g 에 할당한 것인데, 이때 g는 generator 라는 클래스의 객체로서 next() 내장함수를 사용하여 Generator의 다음 값을 계속 가져올 수 있다. Generator는 물론 예제의 마지막 부분과 같이 for 루프에서 사용될 수 있다.

**리스트나 Set과 같은 컬렉션에 대한 iterator는 해당 컬렉션이 이미 모든 값을 가지고 있는 경우이나, Generator는 모든 데이타를 갖지 않은 상태에서 yield에 의해 하나씩만 데이타를 만들어 가져온다는 차이점이 있다.** 이러한 Generator는 데이타가 무제한이어서 모든 데이타를 리턴할 수 없는 경우나, 데이타가 대량이어서 일부씩 처리하는 것이 필요한 경우, 혹은 모든 데이타를 미리 계산하면 속도가 느려서 그때 그때 On Demand로 처리하는 것이 좋은 경우 등에 종종 사용된다.

## 17.3 Generator Expression
Generator Expression은 Generator Comprehension으로도 불리우는데, List Comprehension과 외관상 유사하다. List Comprehension은 앞뒤를 [...] 처럼 대괄호로 표현한다면, Generator Expression (...) 처럼 둥근 괄호를 사용한다. 하지만 Generator Expression은 List Comprehension과 달리 실제 리스트 컬렉션 데이타 전체를 리턴하지 않고, 그 표현식만을 갖는 Generator 객체만 리턴한다. 즉 실제 실행은 하지 않고, 표현식만 가지며 위의 yield 방식으로 Lazy Operation을 수행하는 것이다.

아래 예제는 1부터 1000개까지의 숫자에 대한 제곱값을 Generator Expression으로 표현한 것으로 여기서 Generator Expression을 할당받은 변수 g는 Generator 타입 객체이다. 첫번째 for 루프를 사용하여 10개의 next() 문을 실행하여 처음 10개에 대한 제곱값만을 실행하였다. 두번째 for 루프에서는 11번째부터 마지막까지 모두 실행하게 된다. Generator 객체 g는 상태를 유지하고 있으므로 두번째 for 루프에서 다음 숫자 11부터 계산을 수행한 것이다.

```python
# Generator Expression
g = (n*n for n in range(1001))
 
# g는 generator 객체
print(type(g))  # <class 'generator'>
 
# 리스트로 일괄 변환시
# mylist = list(g)
 
# 10개 출력
for i in range(10):
    value = next(g)
    print(value)
 
# 나머지 모두 출력 
for x in g:
    print(x)
```
