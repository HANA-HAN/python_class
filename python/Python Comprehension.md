# 16. Python Comprehension

## 16.1 Python Comprehension
Python의 Comprehension은 한 Sequence가 다른 Sequence (Iterable Object)로부터 (변형되어) 구축될 수 있게한 기능이다. Python 2 에서는 List Comprehension (리스트 내포)만을 지원하며, Python 3 에서는 Dictionary Comprehension과 Set Comprehension을 추가로 지원하고 있다. 또한, 종종 Generator Comprehension이라고 일컫어 지는 Generator Expression이 있는데, 이는 다음 아티클에서 Generator와 함께 설명한다.

## 16.2 List Comprehension
List Comprehension (리스트 내포)는 입력 Sequence로부터 지정된 표현식에 따라 새로운 리스트 컬렉션을 빌드하는 것으로, 아래와 같은 문법을 갖는다.

```
[출력표현식 for 요소 in 입력Sequence [if 조건식]]
```

여기서 입력 Sequence는 입력으로 사용되는 Iteration이 가능한 데이타 Sequence 혹은 컬렉션이다. 입력 Sequence는 for 루프를 돌며 각각의 요소를 하나씩 가져오게 되고, if 조건식이 있으면 해당 요소가 조건에 맞는지 체크하게 된다. 만약 조건에 맞으면 출력 표현식(Output Expression)에 각 요소를 대입하여 출력 결과를 얻게 된다. 이러한 과정을 모든 요소에 대해 실행하여 결과를 리스트로 리턴하게 된다. 쉽게 설명하면 for 루프를 돌면 특정 조건에 있는 입력데이타를 변형하여 리스트로 출력하는 코드를 간단한 문법으로 표현한 것이다.
아래 예제에서 입력 Sequence (oldlist)는 숫자, 문자 그리고 Boolean 요소를 모두 갖는 리스트이다. List Comprehension 문장을 보면 이 입력 Sequence "oldlist"로부터 요소 i 를 하나씩 가져와 이 i의 타입이 정수형인지 체크하고, 만약 그렇다면 표현식 "i * i" 를 실행하여 i의 제곱을 계산한다. 이렇게 모든 요소에 대해 계산하면 [1, 4, 9] 라는 결과 리스트(newlist)를 얻게 된다.

```python
oldlist = [1, 2, 'A', False, 3]
 
newlist = [i*i for i in oldlist if type(i)==int]
 
print(newlist)
# 출력: [1, 4, 9]
```

## 16.3 Set Comprehension
Set Comprehension은 입력 Sequence로부터 지정된 표현식에 따라 새로운 Set 컬렉션을 빌드하는 것으로, 아래와 같은 문법을 갖는다. List Comprehension과 거의 비슷하지만, 결과가 Set {...}으로 리턴된다는 점이 다르다.

```
{출력표현식 for 요소 in 입력Sequence [if 조건식]}
```

아래 예제에서 입력 Sequence (oldlist)는 중복된 숫자를 갖는 리스트이다. 결과 Set은 중복을 허용하지 않으므로 중복된 데이타는 자연스럽게 제거된다. 또한 Set은 요소의 순서를 보장하지 않으므로, 아래 결과에서 보듯이 순서가 랜덤하게 바뀐 결과를 출력하게 된다.

```python
oldlist = [1, 1, 2, 3, 3, 4]
 
newlist = {i*i for i in oldlist}
 
print(newlist)
# 출력 : {16, 1, 9, 4}
```

## 16.4 Dictionary Comprehension
Dictionary Comprehension은 입력 Sequence로부터 지정된 표현식에 따라 새로운 Dictionary 컬렉션을 빌드하는 것으로, 아래와 같은 문법을 갖는다. Set Comprehension과 거의 비슷하지만, 출력표현식이 Key:Value Pair로 표현된다는 점이 다르며, 결과로 dict 가 리턴된다.

```
{Key:Value for 요소 in 입력Sequence [if 조건식]}
```

아래 예제는 Id로 이름을 찾는 Dictionary (id_name) 를 반대로 Lookup 하기 위해 Key와 Value 서로 바꾼 새로운 Dictionary (name_id) 를 만든 예이다. 새 Dictionary "name_id"는 이름으로 Id를 찾는 Dictionary이다.

```python
id_name = {1: '박진수', 2: '강만진', 3: '홍수정'}
 
name_id = {val:key for key,val in id_name.items()}
 
print(name_id)
 
# 출력 : {'박진수': 1, '강만진': 2, '홍수정': 3}
```

또 다른 예제로 아래는 if 조건식 안에 필터링 함수를 사용한 경우이다. 복잡한 조건식일 경우에는 이처럼 필터링 함수를 사용하면 편리하다. 아래 예제는 1부터 100까지 홀수를 Dictionary Key로 하고, 그 홀수의 제급을 Value로 하는 dict 객체를 생성한다.

```python
def isodd(val):
    return val % 2 == 1
 
mydict = {x:x*x for x in range(101) if isodd(x)}
print(mydict)
```