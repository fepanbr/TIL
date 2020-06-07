## Python 리스트 내장함수



### in

**리스트에 값이 존재하면 True, 존재하지 않으면 False를 반환**

```python
primes = [2, 3, 5, 7, 11, 13, 17, 19, 23]
print(7 not in primes)		# True
print(12 not in primes)		# False
```



### sort, reverse

sort : 리스트를 정렬

reverse: 뒤집어진 순서로 정렬

```python
numbers = [5, 3, 7, 1]
numbers.sort()
print(numbers)		# [1, 3, 5, 7]
numbers.reverse()
print(numbers)		# [7, 5, 3, 1]
```



### index

해당 값을 가지고 있는 원소의 인덱스를 반환해줍니다.



```python
members = ["영훈", "윤수", "태호", "혜린"]
print(members.index("윤수"))		# 1
print(members.index("태호"))		# 2
```



### remove



첫 번째로 해당 원소의 값을 갖고 있는 원소를 삭제합니다.



```python
fruits = ["딸기", "당근", "파인애플", "수박", "참외", "메론"]
fruits.remove("파인애플")
print(fruits)		# ['딸기', '당근', '수박', '참외', '메론']
```

