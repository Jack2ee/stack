1 README.md
============
1. README: README 파일은 프로젝트 저장 페이지를 간결하게 소개하는 페이지이다. 가독성이 좋다는 게 장점이다.
2. README.md: README.md에서 md는 markdown의 준말이다. 마크다운은 페이지를 html파일로 변형시키는 언어이다.

2 stack(참조: https://grepsean.github.io/Algorithms-and-Data-Structures-with-Python-4/)
=======
1. 스택의 개념: 스택은 'LIFO; Last-In, First-Out'즉, 가장 마지막에 저장된 데이터가 가장 먼저 나오는 자료구조이다. 스택에서 데이터를 저장하는 연산을 push, 데이터를 빼내는 연산을 pop이라고 한다.

2. 스택 자료구조의 추상 자료형(ADT):
 + 데이터를 스택에 저장(Push)한다.
 + 데이터를 스택에서 꺼낸다(Pop). 데이터를 Pop하고 나서는 스택에서 해당 데이터는 삭제된다.
 + 데이터를 스택에서 꺼내기전에 잠깐 참조(Peek)할 수 있다. 가장 상위에 저장된 데이터를 보는 것이므로 Peek을 쓰는 것 같다.
 + 데이터가 비어있다면(is_empty), Pop연산을 실행할 수 없다.
 + 데이터가 꽉차 있다면(is_full), Push연산을 실행할 수 없다.(단, 저장할 데이터의 개수를 한정해야 함)
 + 스택에 있는 모든 데이터를 차례대로 출력할 수 있어야 한다.

3. 스택의 구현: ArrayList나 LinkedList, LifoQueue객체를 이용해 구현할 수 있다. 
 + metaClass
```python3
class BaseStackQueue:
    # 데이터의 추가
    def push(self, data):
        raise NotImplemented
    # 데이터의 추가
    def pop(self):
        raise NotImplemented
    # 데이터 참조하기
    def peek(self):
        raise NotImplemented
    # 비어있는지 확인
    def is_empty(self):
        raise NotImplemented
    # 꽉 차있는지 확인
    def is_full(self):
        raise NotImplemented
    # 리스트 전체 출력
    def display(self):
        raise NotImplemented
```

  +ArrayList
 ```python3
 class ArrayStack(BaseStackQueue):
    def __init__(self, max_length=50):
        self.items=[]
        self.top=0 # top에는 데이터를 저장할 최신 위치를 가르킨다.
        self.max_length=max_length
    
    def push(self, data):
        if self.is_full(): # push할 수 있는지 확인
            raise Exception('스택이 꽉 찼습니다!')

        self.items.append(data)
        self.top += 1

    def pop(self):
        if self.is_empty(): # pop할 수 있는지 확인
            raise Exception('스택이 비었습니다!')
        self.top-=1
        data=self.items[self.top]
        del self.items[self.top + 1]
        return data
    
    def peek(self):
        if self.is_empty():
            raise Exception('스택이 비었습니다!')
        return self.items[self.top -1] # pop예정인 데이터를 참조한다.

    def is_empty(self):
        return self.top==0 # top이 0이면, 저장된 데이터가 하나도 없는 것임
    
    def is_full(self):
        # top이 max_length와 동일하다는 것은 꽉 찬것임.
        return self.top == self.max_length

    def display(self):
        for index in range(self.top):
            print(self.items[index])
```
 +LinkedList
```python3
class Liststack(BaseStackQueue):
    def __init__(self, max_length=50):
        self.head = Node()
        self.top = 0
        self.max_length = max_length
    
    def push(self, x):
        if self.is_full():
            raise Exception('스택이 꽉 찼습니다!')
        self.head.next = Node(x, self.head.next) # head의 다음으로 노드를 삽입
        self.top += 1

    def pop(self):
        if self.is_empty():
            raise Exception('스택이 비었습니다!')

        data=self.peek()
        self.top -=1
        self.head.next=self.head.next.next  # head의 다음 노드를 삭제
        return data

    def peek(self):
        if self.is_empty():
            raise Exception('스택이 비었습니다!')
        return self.head.next
    
    def is_empty(self):
        return not self.top

    def is_full(self):
        return self.top==self.max_length
    
    def display(self):
        node = self.head.next
        while node:
            print(node.data)
            node = node.next
```
 + Lifo.Queue
 ```python3
 import queue
 q=queue.LifoQueue()
 q.put() # 큐 객체에 데이터 입력
 q.qsize() # 큐 객체에 저장된 데이터 갯수 데이터 출력
 q.get() # 큐 객체에서 데이터 출력
 q.put_nowait() # 큐 객체가 꽉찬 경우 queue.Full예외 처리
 q.get_nowait() # 큐 객체가 빈 경우 queue.Empty예외 처리
 
 def GetitemList(q):
  ret=[]
  n=q.qsize()
  while n>0:
   ret.append(q.get())
   n-= 1
  return ret
  
