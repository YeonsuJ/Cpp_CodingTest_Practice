# 요세푸스 문제 (권장시간 30분)

## 문제
N명의 사람이 원 형태로 서 있다. 각 사람은 1부터 N까지 번호표를 갖고 있다. 그리고
임의의 숫자 K가 주어졌을 때 다음과 같이 사람을 없앤다.
- 1번 번호표를 가진 사람 기준 시계 방향으로 K번째 사람을 없앤다.
- 없앤 사람 다음 사람을 기준으로 하고 다시 K번째 사람을 없앤다.

N과 K가 주어질 때, 마지막에 살아 있는 사람의 번호를 반환하는 solution() 함수를
구현하라.

## 제약조건
- 1<= N, K <= 1,000 ( N,K은 자연수)

## 입출력 예
|N|K|result|
|------|---|---|
|5|2|3|

## 문제 분석 및 풀이
### 분석
1. 1,2,3,4,5 생존
2. 1기준 , 2번째인 2 제거 (1,3,4,5 생존)
3. 3기준 , 2번째인 4 제거 (1,3,5 생존)
4. 5기준 , 2번째인 1 제거 ( 3, 5 생존)
5. 3기준 , 2번째인 5 제거 ( 3 생존)
   
→

1. front → 1, 2, 3, 4, 5 → rear
2. 1 pop & push , 2 pop (in queue : 3 4 5 1)
3. 3 pop & push , 4 pop (in queue : 5 1 3)
4. 5 pop & push , 1 pop (in queue : 3 5)
5. 3 pop & push , 5 pop (in queue : 3)

## 풀이
<details>
  <summary>펼치기</summary>

```cpp
#include <queue>

using namespace std;

int solution(int N, int K) {
  queue<int> q;
  for (int i = 1; i <= N; i++) {
    q.push(i);
  }

  while (q.size() > 1) {
    for (int i = 0; i < K-1; i++) {
      q.push(q.front());
      q.pop();
    }
    q.pop();
  }
  return q.front();
}
  ```
</details>

## 새롭게 안 사실
- 원형으로 서있으니까 Circular Queue를 쓰는건가?
- c++에서는 STL이 알아서 덱을 사용하여 메모리를 동적으로 할당하고 관리를
최적화해주기 때문에 Linear Queue를 사용함
- c++의 pop은 return void이기 때문에 pop을 먼저 해버리면 data가 사라지기 때문에
push로 rear에 복붙을 먼저 한 다음 버려도 되는 값을 pop

## 시간복잡도 분석
- pop K-1번, push 1번을 N번 반복하므로 최종 시간 복잡도는 O(N*K)
- 세그먼트 트리를 사용하면 시간복잡도를 O(NlogN)으로 개선 가능 (N이 10만이상 커지는 경우)

