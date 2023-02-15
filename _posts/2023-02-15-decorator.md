---
layout: single
title:  "Python Decorator 사용하기"
categories: General
tag: python
lastmod: 2023-02-15
toc: true
author_profile: false
sidebar:
  nav: "docs"
search: true
classes: wide
---

[15분 안에 알아보는 파이썬 데코레이터](https://www.youtube.com/watch?v=r7Dtus7N4pI)

# 매개변수를 데코레이터에 전달


```python
# decorator 정의
def f1(func):
    def wrapper(*args, **kwargs):
        print("Started")
        val = func(*args, **kwargs)
        print("Ended")
        return val

    return wrapper

# decorator 를 이용한 함수 정의
@f1
def f(a, b=9):
    print(a + b)

@f1
def add(x, y):
    return x + y

print(f(10))
print('=' * 10)
print(add(4, 5))
```

    Started
    19
    Ended
    None
    ==========
    Started
    Ended
    9
    

# 데코레이터를 활용한 실행 시간 측정


```python
import time

# decorator 정의
def timer(func):
    def wrapper():
        before = time.time()
        func()
        print(f'Function took: {time.time() - before:.2f} seconds.')

    return wrapper

# decorator 를 이용한 함수 정의
@timer
def run():
    time.sleep(2)


# 함수 호출
run()
```

    Function took: 2.01 seconds.
    

# 데코레이터를 이용한 로그 출력


```python
import datetime

def log(func):
    def wrapper(*args, **kwargs):
        with open('logs.txt', 'a') as file:
            file.write("Called function with " + " ".join([str(arg) for arg in args]) + " at " + str(datetime.datetime.now()) + "\n")

        val = func(*args, **kwargs)
        return val

    return wrapper

@log
def run(a, b, c = 9):
    print(a + b + c)

run(1, 3, c=9)
```

    13
    


```python

```
