# 8. Dictionary

## 8.1 Dictionary (dict)
Dictionary는 "키(Key) - 값(Value)" 쌍을 요소로 갖는 컬렉션이다. Dictionary는 흔히 Map 이라고도 불리우는데, 키(Key)로 신속하게 값(Value)을 찾아내는 해시테이블(Hash Table) 구조를 갖는다.

파이썬에서 Dictionary는 "dict" 클래스로 구현되어 있다. Dictionary의 키(key)는 그 값을 변경할 수 없는 Immutable 타입이어야 하며, Dictionary 값(value)은 Immutable과 Mutable 모두 가능하다. 예를 들어, Dictionary의 키(key)로 문자열이나 Tuple은 사용될 수 있는 반면, 리스트는 키로 사용될 수 없다.

Dictionary의 요소들은 Curly Brace "{...}" 를 사용하여 컬렉션을 표현하는데, 각 요소들은 "Key:Value"" 쌍으로 되어 있으며, 요소간은 콤마로 구분한다. 요소가 없는 빈 Dictionary는 "{}"와 같이 표현한다. 특정 요소를 찾아 읽고 쓰기 위해서는 "Dictionary변수[키]"와 같이 키를 인덱스처럼 사용한다.

```
scores = {"철수": 90, "민수": 85, "영희": 80}
v = scores["민수"]   # 특정 요소 읽기
scores["민수"] = 88  # 쓰기
print(t)
```

파이썬의 Dictionary는 생성하기 위해 위의 예제와 같이 {...} 리터럴(Literal)을 사용할 수도 있지만, 또한 dict 클래스의 dict() 생성자를 사용할 수도 있다. dict() 생성자는 (아래 첫번째 예처럼) Key-Value 쌍을 갖는 Tuple 리스트를 받아들이거나 (두번째 예처럼) dict(key=value, key=value, ...) 식의 키-값을 직접 파라미터로 지정하는 방식을 사용할 수 있다.

```
# 1. Tuple List로부터 dict 생성
persons = [('김기수', 30), ('홍대길', 35), ('강찬수', 25)]
mydict = dict(persons)

age = mydict["홍대길"]
print(age)   # 35

# 2. Key=Value 파라미터로부터 dict 생성
scores = dict(a=80, b=90, c=85)
print(scores['b'])  #90
```

## 8.2 추가, 수정, 삭제, 읽기
Dictionary 요소를 수정하기 위해서는 "Dictionary[키]=새값"와 같이 해당 키 인덱스를 사용하여 새 값을 할당하면 된다. Dictionary에 새로운 요소를 추가하기 위해서는 수정 때와 마찬가지로 ("맵[새키]=새값") 새 키에 새 값을 할당한다. Dictionary 요소를 삭제하기 위해서는 "del 요소"와 같이 하여 특정 요소를 지운다.

```
scores = {"철수": 90, "민수": 85, "영희": 80}
scores["민수"] = 88   # 수정
scores["길동"] = 95   # 추가
del scores["영희"]
print(scores)
# 출력 {'철수': 90, '길동': 95, '민수': 88}
```

Dictionary에 있는 값들을 모두 출력하기 위해서는 다음과 같이 루프를 사용할 수 있다. 아래 예제에서 for 루프는 scores 맵으로부터 키를 하나씩 리턴하게 된다. 이때 키는 랜덤하게 리턴되는데, 이는 해시테이블의 속성이다. 각 키에 따른 값을 구하기 위해서는 scores[key]와 같이 사용한다.

```
scores = {"철수": 90, "민수": 85, "영희": 80}

for key in scores:
    val = scores[key]
    print("%s : %d" % (key, val))
```

## 8.3 유용한 dict 메서드
Dictonary와 관련하여 dict 클래스에는 여러 유용한 메서드들이 있다. dict 클래스의 keys()는 Dictonary의 키값들로 된 dict_keys 객체를 리턴하고, values()는 Dictonary의 값들로 된 dict_values 객체를 리턴한다.

```
scores = {"철수": 90, "민수": 85, "영희": 80}

# keys
keys = scores.keys()
for k in keys:
    print(k)

# values
values = scores.values()
for v in values:
    print(v)
```

dict의 items()는 Dictonary의 키-값 쌍 Tuple 들로 구성된 dict_items 객체를 리턴한다. 참고로 dict_items 객체를 리스트로 변환하기 위해서는 list()를 사용할 수 있다. 이는 dict_keys, dict_values 객체에도 공히 적용된다.

```
scores = {"철수": 90, "민수": 85, "영희": 80}

items = scores.items()
print(items)
# 출력: dict_items([('민수', 85), ('영희', 80), ('철수', 90)])

# dict_items를 리스트로 변환할 때
itemsList = list(items)
```

dict.get() 메서드는 특정 키에 대한 값을 리턴하는데, 이는 Dictionary[키]를 사용하는 것과 비슷하다. 단, Dictionary[키]를 사용하면 키가 없을 때 에러(KeyError)를 리턴하는 반면, get()은 키가 Dictionary에 없을 경우 None을 리턴하므로 더 유용할 수 있다. 물론 get()을 사용하는 대신 해당 키가 Dictionary에 존재하는지 체크하고 Dictionary[키]를 사용하는 방법도 있다. 키가 Dictionary에 존재하는지를 체크하지 위해서는 멤버쉽연산자 in 을 사용하면 된다.

```
scores = {"철수": 90, "민수": 85, "영희": 80}
v = scores.get("민수")  # 85
v = scores.get("길동")  # None
v = scores["길동"]      # 에러 발생

# 멤버쉽연산자 in 사용
if "길동" in scores:
	print(scores["길동"])

scores.clear()  # 모두 삭제
print(scores)
```

dict.update() 메서드는 Dictionary 안의 여러 데이타를 한꺼번에 갱신하는데 유용한 메서드이다. 아래 예제에서 처럼, update() 안에 Dictionary 형태로 여러 데이타의 값을 변경하면, 해당 데이타들이 update() 메서드에 의해 한꺼번에 수정된다.

```
persons = [('김기수', 30), ('홍대길', 35), ('강찬수', 25)]
mydict = dict(persons)

mydict.update({'홍대길':33,'강찬수':26})
```