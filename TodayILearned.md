# **20. 01. 14 THU**

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
# **20. 01. 15 FRI**

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
# **20. 01. 16 SAT**

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
# **20. 01. 17 SUN**

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
# **20. 01. 18 MON**

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
# **20. 01. 19 TUE**

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
# **20. 01. 20 WED**

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

# **20. 01. 22 FRI**

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

# **20. 01. 25 MON**

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

# **20. 01. 26 TUE**

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

# **20. 01. 27 WED**

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

# **20. 01. 28 THU**

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

# **20. 01. 29 FRI**

### List[int] to int
```python
a = [1, 2, 3, 4, 5]
''.join(str(e) for e in a)
''.join(map(str, a))
```

---

# **20. 02. 01 MON**

### [Q.19-역순 연결 리스트 2](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.19-Reverse%20Linked%20List%20II.ipynb)  
제대로 못풀었음. m=1일 경우 스왑 불가능

## 자료 구조
### Queue
FIFO (선입선출, 입장하기 위한 대기줄)
### Stack
LIFO (후입선출, 쌓인 접시)  
None <- 1 <- 2 <- 3 <- 4 <- 5  

# **20. 02. 02 TUE**

### foo in [List]보다 Dict 활용

### [Q.20-유효한 괄호](https://github.com/Yoonkeee/AlgorithmPractice/blob/master/PythonAlgorithmInterview/src/Q.20-Valid%20Parentheses.ipynb) - 아주 우아한 풀이코드의 예시

---

#### 20. 02. 03 ~ 20. 02. 08 이사

# 20 .02. 09 TUE**

### Deque, Priority Queue


# 20 .02. 00 **

### Subtitle

