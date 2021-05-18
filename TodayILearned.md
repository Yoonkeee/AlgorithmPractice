# **21. 01. 14 ~ 16**

A is B 는 객체의 id(주소)값을 비교하는 것 *(object 비교)*  
== 는 값을 비교하는 것 *(value equivalent)*  
None은 값 자체가 없으므로 == 으로 비교할 수 없고, is 로 비교해야 한다  
A = list(리스트)를 하게 되면 리스트를 별도의 객체로 복사하여 다른 ID를 갖게 됨

#### Example 1

``` python
class Negator(object):
    def __eq__(self,other):
        return not other
thing = Negator()
print thing == None  #True
print thing is None  #False
```
#### Example 2

```python
lst = [1,2,3]
lst == lst[:]  # This is True since the lists are "equivalent"
lst is lst[:]  # This is False since they're actually different objects
```

[출처 - Stack Overflow](https://stackoverflow.com/questions/14247373/python-none-comparison-should-i-use-is-or)

---

#### **문자열**

문자열을 다룰 경우 리스트로 매핑하는 과정보다 슬라이싱으로 다루는 것이 속도면에서 훨씬 큰 이점이 있다.  
ex) [Valid Palindrome](https://nbviewer.jupyter.org/github/Yoonkeee/AlgorithmPractice/blob/master/Python%20Algorithm%20Interview/src/Ch.06%20-%2001.%20Valid%20Palindrome.ipynb)

#### **Deque (Double-Ended Queue)**

* deq = collections.deque()   /  from collections import *   ,  deq = deque()  
deq.appendleft(something)  
deq.popleft()  ,  deq.pop()  
queue.pop(0) = deque.popleft() 이지만  
속도는 O(n) << O(1) 이다.  

#### **Reverse**
- Reverse List : (list).reverse()  
- Reverse String : foo = (str)[::-1]

---

#### **2개 이상의 조건**으로 정렬하기

```python
keys: tuple = (key1, key2, ... )
(list).sort(key=keys)
(list).sort(key=some_function)
(list).sort(key=lambda x: (some_lambda))
(list).sort(key=lambda x: ((str).split('.')[1:], (str).split('.'[0]))
foo = sorted((list), key=keys)
```

#### Jupyter Notebook 환경에서 괄호, 따옴표 자동완성 해제 코드

```python
from notebook.services.config import ConfigManager
c = ConfigManager()
c.update('notebook', {"CodeCell": {"cm_config": {"autoCloseBrackets": False}}})
```

---

#### String Cleansing & Max Count
```python
strs = "Bob hit a ball, the hit BALL flew far after it was hit."
words = re.sub(r'[^\w]', ' ', strs).split()
counts = collections.Counter(words).most_common(1)
```
```python
(str).join((str) or (list) or (tuple))
''.join(['1','2','3','4','5']) == '12345'
'+'.join(['1','2','3','4','5']) == '1+2+3+4+5'
```

---
# **21. 01. 18 ~ 24**

### [Tim Sort](https://d2.naver.com/helloworld/0315536)
Python을 포함한 많은 언어에서 Sorting Algorithm으로 사용하는 정렬 방법.  
(Binary)Insertion Sort와 Merge Sort를 결합  
Time Complexity - Best : O(n), Avg : O(nlogn), Worst : O(nlogn)  
Space Complexity - O(n)  
원소를 2개씩 자른 다음  
- i번째 덩어리의 원소가 증가  
  - i+1번째의 덩어리 원소가 증가시 앞의 덩어리에 Binary Insertion sort
  - So on ...
- i+n번째 덩어리의 원소가 감소
  - 감소하는 방향의 새로운 덩어리로 i+n+1, ... 내림차순 정렬
- 생성된 덩어리들을 Merge sort  
  - Galloping - 한 배열에서만 계속 병합이 이뤄질 경우 참조 index = 2^k로 증가  

---

### 문자열 슬라이싱 
s == s[::-1]  => 문자열 뒤집기, 속도가 매우 빠름  
```python
(str)[::-1 ] == reverse(s)
if len(s) < 2 or s == s[::-1]:
    return s
```

### **Sliding Window** with Two Pointer
```python
for i in range(0, len(s)-1):
    result = max(resunt,
                 expand(s, i, i+1),
                 expand(s, i, i+2),
                 key=len)
  return result
```

---

### Time Complexity of **in**
```python
var in some_list  # O(n)
var in some_dict  # O(1) , Search KEY
```
### 함수 호출시 Callable(lambda)을 인자로 넣을 수 있음
```python
this_is_lambda = lambda : print('lambda')
some_func(this_is_lambda)
```
### Typing
```python
list_or_something:Iterable[int] = [1,2,3]
some_list:list_or_something = [5,5,5]
connection_options = dict[str, str]
ADDRESS = tuple[str, int]
server = tuple[ADDRESS, connection_options]
```

---

### Two Pointer Moving (=Sliding Window)  
[Q.07 두 수의 합](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.07-Two%20Sum.ipynb)  
[Q.08 빗물 트래핑](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.08-Trapping%20Rain%20Water.ipynb)  
[Q.09 세 수의 합](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.09-Three%20Sum.ipynb)  

### List Slicing
```python
l = [1,2,3,4,5,6,7]
[n for i, n in enumerate(l) if i%2 == 0] == l[::2] == [2,4,6]  # 짝수번째 값들만 얻은 것
```

---

# **21. 01. 25 ~ 31**

### Linked List in Python
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

head = ListNode(1)
head.next = ListNode(2)
print(head.next.val == 2)
head.next.next = ListNode(3)
print(head.next.next.val == 3)
```

Linked List는 List로 변형 후 다루는 것이 편리  
deque는 양방향 모두 O(1)에 pop 가능!!  
deque.popleft() faster than que.pop(0)  

---

### [연산의 실행 순서](https://wikidocs.net/20708)

순위 | 연산자 | 설명
---|---|---
1	|(), {}, []	|Tuple, Set, List, Dictionary
2	|collection[index] <br> collection[index1, index2] <br> function(aguments ...) <br> object.attribute	|컬렉션의 첨자 <br> 슬라이싱 <br> 함수의 인수 <br> 객체의 속성 등
3	|**	|거듭제곱
4 |	+ , - , ~	| 단항 연산자(부호, bitwise not)
5	| * / // %	| 곱하기, 나누기, 정수 몫, 나머지
6	| + -	| 더하기, 빼기
7	| << >>	| 시프트 연산
8	| &	| bitwise and
9	| ^	| bitwise xor
10 | | 		
11	| in, not in <br> is, is not <br> <, <=, >, >=, ==, !=	| 멤버 연산자 <br>아이디 연산자 <br> 관계 연산자
12	| not	| 논리 not
13	| and	| 논리 and
14	| or	| 논리 or
15	| if else	| 삼항 연산자
16	| lambda	| 람다 표현식

---

### Linked List 생성하기
```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
        
input_data = [[1, 2, 4], [1, 3, 4]]
heads:List[ListNode] = []

for i in range(len(input_data)):
    if len(input_data) >= 1:
        head = ListNode(input_data[i][-1])
        for n in range(-2, -len(input_data[i])-1, -1):
            node = head
            head = ListNode(input_data[i][n])
            head.next = node
        heads.append(head)
    else:
        heads.append([])
```
---

### Linked List 조작  
[Q.15-역순 연결 리스트](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.15-Reverse%20Linked%20List.ipynb)    
현재 node를 따로 저장 후 활용하는 방법
```python
next, node.next = node.next, prev
prev, node = node, next
```
---
root node를 저장해두고 root.next부터 활용하는 방법도 있음.  
연결 리스트의 포인터 스왑을 더 능숙하게 연습할 필요가 있음.

### List[int] to int
```python
a = [1, 2, 3, 4, 5]
''.join(str(e) for e in a)
''.join(map(str, a))
```

---

# **21. 02. 01 ~ 7**

### [Q.19-역순 연결 리스트 2](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.19-Reverse%20Linked%20List%20II.ipynb)  
제대로 못풀었음. m=1일 경우 스왑 불가능

## 자료 구조
### Queue
FIFO (선입선출, 입장하기 위한 대기줄)
### Stack
LIFO (후입선출, 쌓인 접시)  
None <- 1 <- 2 <- 3 <- 4 <- 5  

### foo in [List]보다 Dict 활용

### [Q.20-유효한 괄호](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.20-Valid%20Parentheses.ipynb) - 아주 우아한 풀이코드의 예시

---

#### 21. 02. 03 ~ 21. 02. 08 이사

# **21. 02. 09 ~ 14**

### Deque, Priority Queue
Priority Que = 다익스트라 알고리즘(최단경로), 힙 구조와 관련  

### PriorityQueue, heapq
[Q.27-Merge k Sorted Lists](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.27-Merge%20k%20Sorted%20Lists.ipynb) - heapq 사용(다시보기)

### PriorityQueue vs heapq  
굳이 우선순위 큐를 사용할 필요 없이 heapq 사용하면 됨.

### heapq 사용법  
``` python
li = [5,4,3,2,1]  
heapq.heapify(li)  
heapq.heappop(li)  
heapq.heappush(li, 6)
```
heap*을 수행할 때마다 heap 구조로 이진트리 재배치함  

### Max Heapq
``` python
import heapq

nums = [4, 1, 7, 3, 8, 5]
heap = []

for num in nums:
  heapq.heappush(heap, (-num, num))  # (우선 순위, 값)

while heap:
  print(heapq.heappop(heap)[1])  # index 1
```
(-num, num)을 활용하여 음수를 취하면 Max Heapq 구조

# **21. 02. 15 ~ 21**

## 해시
임의 크기 데이터를 고정 크기 값으로 매핑
### 장점
분할 상환 분석에 따른 시간 복잡도가 O(1)  
데이터 양에 관계 없이 빠른 성능  

### 해시값 충돌 해결 방법
1. 개별 체이닝  
  충돌하는 경우 연결 리스트로 묶음
2. 오픈 어드레싱  
  충돌 발생 시 다른 빈 공간에 저장  
  선형 탐사의 경우 데이터가 뭉치는 경향이 발생(클러스터링)  
  기준이 되는 로드 팩터 비율을 넘어서게 되면 그로스 팩터의 비율에 따라 더 큰 크기의 버킷으로 이사감.  

**!! 파이썬에서 해시 테이블로 구성된 자료형은 딕셔너리 자료형이다**  
개별 체이닝은 추가 메모리가 필요하며 상대적으로 속도가 느린 추가 메모리 할당이 필요하므로, __파이썬에서는 오픈 어드레싱으로 사용했다.__
(파이썬의 로드 팩터는 0.66, 자바는 0.75)


# **21. 02. 22 ~ 28**

### [Q.30 투 포인터 문제](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.30-Longest%20Substring%20Without%20Repeating%20Characters.ipynb)
다시 풀어보자.

### Sort
```python
foo = sorted(bar:list, key = lambda x:(some_func))
```

### Counter.most_common(k)
Counter에서 빈도 수가 높은 순서대로 아이템을 추출하는 기능인 most_common()


## 비선형 자료구조
### 그래프
- 해밀턴 경로 : 한 번만 방문하는 경로
- 해밀턴 순환 : 한 번만 방문하여 출발지로 돌아오는 경로
- 외판원 문제 : 한 번만 방문하여 출발지로 돌아오는 경로 중 가장 짧은 경로  

### 그래프 순회 (그래프 탐색)
- DFS (깊이 우선 탐색)  
  주로 스택, 재귀, 백트래킹으로 구현
  #### **recursive**
  ```python
  def recursive_dfs(v, discovered=[]):
      discovered.append(v)
      for w in graph[v]:
          if not w in discovered:
              discovered = recursive_dfs(w, discovered)
      return discovered
  ```
  #### **stack**
  ```python
    def iterative_dfs(start_v):
        discovered = []
        stack = [start_v]
        while stack:
            v = stack.pop()
            if v not in discovered:
                discovered.append(v)
                for w in graph[v]:
                    stack.append(w)
        return discovered
  ```
- BFS (너비 우선 탐색)  
  큐로 구현, 최단 경로, 다익스트라. *재귀 구현 불가*
  #### **queue**
  ```python
  def iterative_bfs(start_v):
      discovered = [start_v]
      queue = [start_v]
      while queue:
          v = queue.pop(0)
          for w in graph[v]:
              if w not in discovered:
                  discovered.append(w)
                  queue.append(w)
      return discovered
  ```
#### [Q.32 동서남북 DFS](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.32-Number%20of%20Islands.ipynb)

#### [Q.34 순열 Permutations DFS](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.34-Permutations)

### itertools - permutations, combinations
```python
list(map(list, itertools.permutations(nums)))
list(map(list, itertools.combinations(range(1, n+1), k)))
```
# **21. 03. 01 ~ 07**

#### [Q.36 조합의 합 DFS](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.36-Combination%20Sum.ipynb)
#### [Q.39 코스 스케줄 DFS](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.39-Course%20Schedule.ipynb) - 가지치기로 시간복잡도 최적화

## 최단 경로 문제  
- 다익스트라 알고리즘  
  **BFS(너비 우선 탐색)**  
  항상 노드 주변의 최단 경로만을 택하는 대표적인 Greedy Algorithm중 하나로, 단순하며 실행 속도 또한 빠르다.  
  #### [Q.40 네트워크 딜레이 - 다익스트라](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.40-Network%20Delay%20Time.ipynb) 기본적인 개념이므로 다시 풀어보기
```python
heapq.heappop(list)  # heappop 한번만 해도 heapify됨
```

# **21. 03. 08 ~ 14**

#### [Q.41 K 경유지](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.41-Cheapest%20Flights%20Within%20K%20Stops.ipynb) - 조건이 조금 다른 다익스트라

- #### 순열
  ```python
  map(list, itertools.permutations(nums))
  ```

#### 변수의 범위
```python
def test1():
    v1 = 10
    print(f'print v1 at test1() : {v1}')  # = 10
    def test2():
        nonlocal v1
        print(f'print v1 at test2() : {v1}')  # = 10
        v1 = 50
        print(f'print v1 after reassign v1 = 50 : {v1}')  # = 50
    test2()
    print(f'print v1 after test2() : {v1}')  # = 50
test1()
```   
- nonlocal을 선언하지 않고 reassign도 없다면 사용 가능
- nonlocal을 선언하지 않고 reassign한다면 해당 함수의 지역 변수로 판단하여 **UnboundLocalError: local variable 'v1' referenced before assignment** 에러 생성
- nonlocal을 선언 후 reassign하면 바깥의 변수 v1에 접근  

#### **global과 nonlocal의 차이를 기억하자.**

# **21. 03. 15 ~ 21**


## [* (Astreisk) 이해하기](https://mingrammer.com/understanding-the-asterisk-of-python/)
### 가변 인자를 사용할 때
- #### positional arguments만 받을 때
```python
def save_ranking(*args):
    print(args)
save_ranking('ming', 'alice', 'tom', 'wilson', 'roy')
# ('ming', 'alice', 'tom', 'wilson', 'roy')
```
- #### keyword arguments만 받을 때
```python
def save_ranking(**kwargs):
    print(kwargs)
save_ranking(first='ming', second='alice', fourth='wilson', third='tom', fifth='roy')
# {'first': 'ming', 'second': 'alice', 'fourth': 'wilson', 'third': 'tom', 'fifth': 'roy'}
```
- #### positional arguments와 keyword arguments를 모두 받을 때
```py
def save_ranking(*args, **kwargs):
    print(args)
    print(kwargs)
save_ranking('ming', 'alice', 'tom', fourth='wilson', fifth='roy')
# ('ming', 'alice', 'tom')
# {'fourth': 'wilson', 'fifth': 'roy'}
```
### 컨테이너 타입의 데이터를 Unpacking 할 때
```py
from functools import reduce

primes = [2, 3, 5, 7, 11, 13]

def product(*numbers):
    p = reduce(lambda x, y: x * y, numbers)
    return p

product(*primes)
# 30030

product(primes)
# [2, 3, 5, 7, 11, 13]
```
- 함수의 인자로써 사용하는게 아닌 리스트나 튜플 데이터를 다른 변수에 가변적으로 unpacking 하여 사용하는 형태
```py
numbers = [1, 2, 3, 4, 5, 6]

# unpacking의 좌변은 리스트 또는 튜플의 형태를 가져야하므로 단일 unpacking의 경우 *a가 아닌 *a,를 사용
*a, = numbers
# a = [1, 2, 3, 4, 5, 6]

*a, b = numbers
# a = [1, 2, 3, 4, 5]
# b = 6

a, *b, = numbers
# a = 1
# b = [2, 3, 4, 5, 6]

a, *b, c = numbers
# a = 1
# b = [2, 3, 4, 5]
# c = 6
```

## 2차원 list를 1차원 list로 변형
```py
my_list = [[1, 3, 4, 5],
           [6, 2, 9, 9],
           [4, 3,10, 5],
           [5, 2, 8, 6]]

my_list = [foo for bar in my_list for foo in bar]
```

## 2차원 list에서 좌/우측 선택
```py
width = len(my_list)
my_list = [foo for bar in my_list for foo in bar]
left_list = [x for i,x in enumerate(my_list) if i%width < width//2]
right_list = [x for i,x in enumerate(my_list) if i%width >= width//2]
```

# **21. 03. 22 ~ 28**

## 트리
- 트리란 순환 구조를 갖지 않는 그래프이다.  
- 부모 노드는 단 하나여야 한다.
- 루트는 하나여야 한다.

[Q.43 이진 트리 직경](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.43-Diameter%20of%20Binary%20Tree.ipynb)  

[Q.45 이진 트리 반전](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.45-Invert%20Binary%20Tree.ipynb) - Queue를 활용한 BFS, Stack을 활용한 DFS  


# **21 .03. 29 ~ 04. 03**

### [Database Application Project](https://github.com/Yoonkeee/2021SS_DatabaseApplication)


# **21 .04. 04 ~ 10**

### [Database Application Project](https://github.com/Yoonkeee/2021SS_DatabaseApplication)


# **21 .04. 11 ~ 17**

### [Database Application Project](https://github.com/Yoonkeee/2021SS_DatabaseApplication)

## Class inspect

### [inspect.getargvalues(frame)](https://docs.python.org/3/library/inspect.html#inspect.getargvalues)
Get information about arguments passed into a particular frame.  
A named tuple ArgInfo(args, varargs, keywords, locals) is returned.  
args is a list of the argument names.  
varargs and keywords are the names of the * and ** arguments or None.  
locals is the locals dictionary of the given frame.  

Example  
```py
function_input_params = inspect.getargvalues(inspect.currentframe())[3]
```

# **21 .04. 18 ~ 24**

### [Database Application Project](https://github.com/Yoonkeee/2021SS_DatabaseApplication)  


# **21 .04. 25 ~ 05. 01**

### [Database Application Project](https://github.com/Yoonkeee/2021SS_DatabaseApplication)  

[Q.49 최소 높이 트리](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.48-Balanced%20Binary%20Tree.ipynb) - Depth of Tree 계산  

# **21 .05. 2 ~ 08**

[Q.51 이진 탐색 트리를 더 큰 수 합계 트리로](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.51-Binary%20Search%20Tree%20to%20Greater%20Sum%20Tree.ipynb) - Tree 순회  

[Q.52 이진 탐색 트리(BST) 합의 범위](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.52-Range%20Sum%20of%20BST.ipynb) - Tree 조건부 순회(DFS, BFS)

```python
sys.maxsize, -sys.maxsize  # int형 최대 크기
# float('inf'), float('-inf')가 더 큼
```
## 트리 순회

- ### 전위 순회의 재귀 구현
```py
def preorder(node):
  if node is None:
    return
  print(node.val)
  preorder(node.left)
  preorder(node.right)
```   
- ### 중위 순회의 재귀 구현
```py
def inorder(node):
  if node is None:
    return
  inorder(node.left)
  print(node.val)
  inorder(node.right)
```
- ### 전위 순회의 재귀 구현
```py
def postorder(node):
  if node is None:
    return
  postorder(node.left)
  postorder(node.right)
  print(node.val)
```

[Q.54 전위, 중위 순회로 이진 트리 구축](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.54-Construct%20Binary%20Tree%20from%20Preorder%20and%20Inorder%20Traversal.ipynb) - 2가지의 트리 순회 결과로 이진트리 구축하기. 개념 이해가 어려웠음.  

## 힙 (Heap)
- 0번째 인덱스는 사용하지 않는 것이 국룰  
- 다익스트라 알고리즘에 사용하여 O(V^2) -> O(E log V)로 줄어듬  
- 추출시 다시 힙의 특성을 유지하도록 스와핑이 일어나기 때문에 O(log n)  

```py
nums = [1,2,3,4,5,6,7]
k = 3
# nlargest : n번째 큰 값
heapq.nlargest(k, nums)  # [7,6,5]
# nsmallest : n번째 작은 값
heapq.nsmallest(k, nums)  # [1,2,3]
```

## 트라이 (Trie)  
- 검색 트리의 일종으로 일반적으로 키가 문자열인, 동적 배열 또는 연관 배열을 저장하는 데 사용되는 정렬된 트리 자료구조  
- 트리의 이진 트리의 모습이 아닌 다진 트리의 형태  

## **우선순위 스케쥴링 알고리즘**  

[Q.79 키에 따른 대기열 재구성](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.79-Queue%20Reconstruction%20by%20Height.ipynb) - 우선순위 큐를 사용한 기본적인 정렬  

[Q.80 태스크 스케줄러](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.80-Task%20Scheduler.ipynb) - Counter를 Max Heap처럼 사용  

### collections.Counter()
```py
counter = collectnios.Counter(tasks)
# most_common(n) : 가장 많은 아이템부터 n회 추출, 사실상 Max Heap과 같은 역할
for task, _ in counter.most_common(n+1):  
  counter.subtrack(task)  # heappop()처럼 사용된 task의 couter를 -1해줌
  counter += collections.Counter()  # count가 0 이하인 아이템을 삭제
```

[Q.81 주유소](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.81-Gas%20Station.ipynb) - 회전 방문, 출발지 결정 (책 풀이 - 2번 참고)  

[Q.82 쿠키 부여](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.82-Assign%20Cookies.ipynb) - bisect 이진 검색?

eval(expression) : 문자열을 파싱하여 표현식으로 처리해주는(Evaluate) 역할 수행  

```py
exp = '4+5'
eval(exp)  # 9
```

[Q.84 괄호를 삽입하는 여러 가지 방법](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.84-Different%20Ways%20to%20Add%20Parentheses.ipynb) - 분할 정복 기초  



# **21 .05. 09 ~ 15**

### [Q.57 팰린드롬 페어](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.57-Palindrome%20Pairs.ipynb) - Trie 구조로 팰린드롬 판별 난이도 🌟🌟🌟  


# **21 .05. 16 ~ 21**

### 


<!--

# **21 .05. 00 ~ 00**

### Subtitle

-->