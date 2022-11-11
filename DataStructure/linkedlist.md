# 연결리스트 (LinkedList)

LinkedList는 엘리먼트와 엘리먼트 간의 연결을 이용해서 리스트를 구현함

**Node**라고 하는 데이터, 주소로 이루어진 클래스를 만들어 연결하는 것이 핵심.  
노드는 이전의 노드와 다음 노드로, 즉 객체끼리 연결되어 있어 엘리먼트를 검색하는 과정도 이처럼 하나씩 물어물어 간다.  
이 때문에 Memory Address도 ArrayList와 달리 흩어져있다.

이러한 노드의 성격 때문에 데이터의 **검색은 성능이 떨어진다**.

반면 **데이터를 추가/삭제**하는 경우, 노드 간의 연결을 새로 이어주거나 끊으면 되기 때문에 **성능이 좋다**.