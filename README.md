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

3. 스택의 구현: ArrayList나 LinkedList를 이용해 구현할 수 있다. 
  '''python
  class BaseStackQueue:
    # 데이터의 추가
    def push(self, data):
        raise NotImplemented
    # 데이터 꺼내오기
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
    '''
