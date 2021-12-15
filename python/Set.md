# 9. Set

## 9.1 Set
Set은 중복이 없는 요소들 (unique elements)로만 구성된 집합 컬렉션이다. Set은 Curly Brace { } 를 사용하여 컬렉션을 표현하는데, 내부적으로 요소들을 순서대로 저장하기 않기 때문에, 순서에 의존하는 기능들을 사용할 수 없다. 만약 set을 정의할 때, 중복된 값을 입력하는 경우, set은 중복된 값을 한번만 가지고 있게 된다. 리스트나 튜플 등을 set으로 변경하기 위해서는 set() 생성자를 사용한다. 이는 리스트에 중복된 값들이 있을 때, 중복 없이 Unique한 값만을 얻고자 할 때 유용하다.

```python
# set 정의
myset = { 1, 1, 3, 5, 5 }
print(myset)    # 출력: {1, 3, 5}
 
# 리스트를 set으로 변환
mylist = ["A", "A", "B", "B", "B"]
s = set(mylist)
print(s)        # 출력: {'A', 'B'}
```

## 9.2 Set에서의 추가 및 삭제
Set에 하나의 새로운 요소를 추가하기 위해서는 set 클래스의 add() 메서드를 사용하고, 여러 개의 요소들을 한께번에 추가하기 위해서는 update() 메서드를 사용한다. 또한 Set에서 하나의 요소를 삭제하기 위해서는 remove() 혹은 discard() 메서드를 사용하고, 전체를 모두 지우기 위해서는 clear() 메서드를 사용한다.

```python
myset = {1, 3, 5}
 
# 하나만 추가
myset.add(7)
print(myset)
 
# 여러 개 추가
myset.update({4,2,10})
print(myset)
 
# 하나만 삭제
myset.remove(1)
print(myset)
 
# 모두 삭제
myset.clear()
print(myset)
```

## 9.3 집합 연산
수학에서 두개의 집합 간의 연산으로 교집합, 합집합, 차집합이 있는데, set 클래스는 이러한 집합 연산 기능을 제공한다. 즉, a와 b가 set 일 때, 교집합은 a & b (혹은 a.intersection(b)), 합집합은 a | b (혹은 a.union(b)), 차집합은 a - b (혹은 a.differene) 와 같이 구할 수 있다.

```python
a = {1, 3, 5}
b = {1, 2, 5}
 
# 교집합
i = a & b
# i = a.intersection(b)
print(i)
 
# 합집합
u = a | b
# u = a.union(b)
print(u)
 
# 차집합
d = a - b
# d = a.difference(b)
print(d)
```