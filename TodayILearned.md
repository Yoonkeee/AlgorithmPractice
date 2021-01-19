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


# **20. 01. 19 TUE**

### Title


























