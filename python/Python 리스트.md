### Python 리스트



#### 기본적인 python에서 리스트

```python
numbers = [1, 2, 3, 4, 5]

print(numbers)		# [1, 2, 3, 4, 5]
print(numbers[0])	# 1
print(numbers[-1])	# 5
print(numbers[5])	# error
print(number[-6])	# error
```



#### 리스트를 일부만 사용 (Slice)



````python
numbers = [1, 2, 3, 4, 5, 6]

print(numbers[0:3])		## [1, 2, 3, 4]
print(numbers[1:])		## [2, 3, 4, 5, 6]
print(nubmers[:3])		## [1, 2, 3, 4]
````



#### 원소 바꾸기



```python
numbers = [1, 2, 3, 4, 5, 6]

numbers[0] = 7
print(numbers);		# [7, 1, 2, 3, 4, 5, 6]
# -------------------------------------------- #

numbers[0] = numbers[0] + numbers[1]
print(numbers)		## [3, 2, 3, 4, 5, 6]
```

