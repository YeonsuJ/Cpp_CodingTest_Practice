## 문제 설명

코딩테스트를 준비하는 머쓱이는 프로그래머스에서 문제를 풀고 나중에 다시 코드를 보면서 공부하려고 작성한 코드를 컴퓨터 바탕화면에 아무 위치에나 저장해 둡니다. 저장한 코드가 많아지면서 머쓱이는 본인의 컴퓨터 바탕화면이 너무 지저분하다고 생각했습니다. 
프로그래머스에서 작성했던 코드는 그 문제에 가서 다시 볼 수 있기 때문에 저장해 둔 파일들을 전부 삭제하기로 했습니다.

컴퓨터 바탕화면은 각 칸이 정사각형인 격자판입니다. 이때 컴퓨터 바탕화면의 상태를 나타낸 문자열 배열 wallpaper가 주어집니다. 
파일들은 바탕화면의 격자칸에 위치하고 바탕화면의 격자점들은 바탕화면의 가장 왼쪽 위를 (0, 0)으로 시작해 (세로 좌표, 가로 좌표)로 표현합니다. 
빈칸은 ".", 파일이 있는 칸은 "#"의 값을 가집니다. 드래그를 하면 파일들을 선택할 수 있고, 선택된 파일들을 삭제할 수 있습니다. 
머쓱이는 최소한의 이동거리를 갖는 한 번의 드래그로 모든 파일을 선택해서 한 번에 지우려고 하며 드래그로 파일들을 선택하는 방법은 다음과 같습니다.

- 드래그는 바탕화면의 격자점 S(lux, luy)를 마우스 왼쪽 버튼으로 클릭한 상태로 격자점 E(rdx, rdy)로 이동한 뒤 마우스 왼쪽 버튼을 떼는 행동입니다.
이때, "점 S에서 점 E로 드래그한다"고 표현하고 점 S와 점 E를 각각 드래그의 시작점, 끝점이라고 표현합니다.

- 점 S(lux, luy)에서 점 E(rdx, rdy)로 드래그를 할 때, "드래그 한 거리"는 |rdx - lux| + |rdy - luy|로 정의합니다.

- 점 S에서 점 E로 드래그를 하면 바탕화면에서 두 격자점을 각각 왼쪽 위, 오른쪽 아래로 하는 직사각형 내부에 있는 모든 파일이 선택됩니다.

예를 들어 wallpaper = [".#...", "..#..", "...#."]인 바탕화면을 그림으로 나타내면 다음과 같습니다.

<img width="331" height="218" alt="image" src="https://github.com/user-attachments/assets/c42a79ae-fd60-4889-9792-3a510329b6e9" />

이러한 바탕화면에서 다음 그림과 같이 S(0, 1)에서 E(3, 4)로 드래그하면 세 개의 파일이 모두 선택되므로 
드래그 한 거리 (3 - 0) + (4 - 1) = 6을 최솟값으로 모든 파일을 선택 가능합니다.

<img width="339" height="220" alt="image" src="https://github.com/user-attachments/assets/ca40384a-3df8-4731-8bd6-364de2474233" />

(0, 0)에서 (3, 5)로 드래그해도 모든 파일을 선택할 수 있지만 이때 드래그 한 거리는 (3 - 0) + (5 - 0) = 8이고 이전의 방법보다 거리가 늘어납니다.

머쓱이의 컴퓨터 바탕화면의 상태를 나타내는 문자열 배열 wallpaper가 매개변수로 주어질 때 바탕화면의 파일들을 한 번에 삭제하기 위해 최소한의 이동거리를 갖는 
드래그의 시작점과 끝점을 담은 정수 배열을 return하는 solution 함수를 작성해 주세요. 
드래그의 시작점이 (lux, luy), 끝점이 (rdx, rdy)라면 정수 배열 [lux, luy, rdx, rdy]를 return하면 됩니다.


## 제한사항

- 1 ≤ wallpaper의 길이 ≤ 50
- 1 ≤ wallpaper[i]의 길이 ≤ 50
  - wallpaper의 모든 원소의 길이는 동일합니다.
- wallpaper[i][j]는 바탕화면에서 i + 1행 j + 1열에 해당하는 칸의 상태를 나타냅니다.
- wallpaper[i][j]는 "#" 또는 "."의 값만 가집니다.
- 바탕화면에는 적어도 하나의 파일이 있습니다.
- 드래그 시작점 (lux, luy)와 끝점 (rdx, rdy)는 lux < rdx, luy < rdy를 만족해야 합니다.

## 입출력 예
|wallpaper|result|
|---|---|
|[".#...", "..#..", "...#."]|[0, 1, 3, 4]|
|["..........", ".....#....", "......##..", "...##.....", "....#....."]|[1, 3, 5, 8]|
|[".##...##.", "#..#.#..#", "#...#...#", ".#.....#.", "..#...#..", "...#.#...", "....#...."]|[0, 0, 7, 9]|
|["..", "#."]|[1, 0, 2, 1]|

## 입출력 예 설명
입출력 예 #1
- 문제 설명의 예시와 같은 예제입니다. (0, 1)에서 (3, 4)로 드래그 하면 모든 파일을 선택할 수 있고 드래그 한 거리는 6이었고, 6보다 적은 거리로 모든 파일을 선택하는 방법은 없습니다. 따라서 [0, 1, 3, 4]를 return합니다.

입출력 예 #2
- 예제 2번의 바탕화면은 다음과 같습니다.
<img width="649" height="343" alt="image" src="https://github.com/user-attachments/assets/740a6116-5421-40d9-a0d9-db689ca5fa44" />

(1, 3)에서 (5, 8)로 드래그하면 모든 파일을 선택할 수 있고 이보다 적은 이동거리로 모든 파일을 선택하는 방법은 없습니다.
따라서 가장 적은 이동의 드래그로 모든 파일을 선택하는 방법인 [1, 3, 5, 8]을 return합니다.

입출력 예 #3
- 예제 3번의 바탕화면은 다음과 같습니다.
<img width="594" height="467" alt="image" src="https://github.com/user-attachments/assets/fcfce1b1-b15f-4694-9114-bb27b47ad494" />

모든 파일을 선택하기 위해선 바탕화면의 가장 왼쪽 위 (0, 0)에서 가장 오른쪽 아래 (7, 9)로 드래그 해야만 합니다. 따라서 [0, 0, 7, 9]를 return합니다.

입출력 예 #4
- 예제 4번의 바탕화면은 다음과 같이 2행 1열에만 아이콘이 있습니다.
<img width="174" height="162" alt="image" src="https://github.com/user-attachments/assets/b1bb4741-20ea-43cf-aa72-8f3fbbaaba30" />

이를 드래그로 선택하기 위해서는 그 칸의 왼쪽 위 (1, 0)에서 오른쪽 아래 (2, 1)로 드래그 하면 됩니다. (1, 0)에서 (2, 2)로 드래그 해도 아이콘을 선택할 수 있지만 이전보다 이동거리가 늘어납니다. 
따라서 [1, 0, 2, 1]을 return합니다.

## 풀이 1
<details>
  <summary>펼치기 </summary>

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> solution(vector<string> wallpaper) {
    vector<int> answer;
    int lux=51, luy=51;
    int rdx=0, rdy=0;
    
    for(int i=0; i<wallpaper.size(); i++){
        for(int j=0; j<wallpaper[i].size(); j++){
            
            if(wallpaper[i][j] == '#'){
                lux = min(lux,i);
                luy = min(luy,j);
                
                rdx = max(rdx, i+1);
                rdy = max(rdy, j+1);
            }
        }
    }
    
    return {lux, luy, rdx, rdy};
}
```
</details>

### 접근법 및 배운 점 1
- 최소 직사각형 찾기: 흩어져 있는 파일들(#)을 한 번의 드래그로 모두 선택하려면,
- 파일이 존재하는 위치들의 가장 상단(min x), 가장 좌측(min y), 가장 하단(max x), 가장 우측(max y) 좌표를 구해야 함
- 완전 탐색 : wallpaper의 크기가 최대 50x50으로 매우 작으므로, 이중 반복문을 통해 모든 칸을 확인해도 시간 복잡도상 문제가 없음
- 좌표 갱신:
  - 시작점 (lux, luy): 파일이 발견될 때마다 현재 인덱스와 비교하여 최솟값으로 갱신 (초기값은 최대 범위보다 큰 51로 설정)
  - 끝점 (rdx, rdy): 파일이 발견될 때마다 현재 인덱스와 비교하여 최댓값으로 갱신
 
- 격자점과 칸의 좌표 개념 차이:
  - 파일은 (i, j) 칸에 존재하지만, 이를 포함하는 드래그의 끝점은 해당 칸의 오른쪽 아래 모서리인 (i + 1, j + 1)이어야 함
  - 따라서 rdx, rdy를 갱신할 때는 단순히 i, j가 아니라 i + 1, j + 1과 비교해야 한다는 점이 핵심
- 초기값 설정의 중요성: 최솟값을 구할 변수(lux, luy)는 가능한 범위보다 큰 값으로, 최댓값을 구할 변수(rdx, rdy)는 0으로 초기화해야 올바르게 갱신됨
- <algorithm> 헤더의 min, max 함수를 사용하여 if를 여러 번 쓰는 것보다 코드를 훨씬 간결

## 풀이 2
<details>
  <summary>펼치기 </summary>

```cpp
#include <string>
#include <vector>
#include <algorithm> // min_element, max_element가 포함된 헤더

using namespace std;

vector<int> solution(vector<string> wallpaper) {
    vector<int> rows; // 파일이 있는 행(세로) 좌표들만 모음
    vector<int> cols; // 파일이 있는 열(가로) 좌표들만 모음
    
    // 1. 모든 칸을 돌며 파일('#')의 좌표를 수집
    for(int i=0; i<wallpaper.size(); i++){
        for(int j=0; j<wallpaper[i].size(); j++){
            if(wallpaper[i][j] == '#'){
                rows.push_back(i);
                cols.push_back(j);
            }
        }
    }
    
    // 2. 수집된 좌표들 중에서 최소/최대값 찾기
    // min_element와 max_element는 '이터레이터(주소값)'를 반환하므로 
    // 앞에 *(참조 연산자)를 붙여서 실제 값을 가져와야 함
    
    int lux = *min_element(rows.begin(), rows.end());
    int luy = *min_element(cols.begin(), cols.end());
    
    // 끝점은 해당 칸의 우측 하단이므로 +1
    int rdx = *max_element(rows.begin(), rows.end()) + 1; 
    int rdy = *max_element(cols.begin(), cols.end()) + 1;
    
    return {lux, luy, rdx, rdy};
}
```
</details>

### 접근법 및 배운 점 2
- 동작 원리
  - min_element(begin, end): 범위 내에서 가장 작은 원소를 가리키는 이터레이터를 반환
  - 값에 접근하려면 * (역참조 연산자) 필요함
- 장점
  - if (min_val > current) min_val = current; 와 같은 비교 조건문을 직접 짤 필요가 없어 코드가 직관적
  - 좌표 수집 단계와 계산 단계가 분리되어 로직이 명확해 보일 수 있음
- 단점(주의)
  - 메모리 사용: 풀이1 방식(변수 4개만 사용)과 달리, 파일(#)이 많을 경우 rows, cols 벡터에 좌표를 모두 저장해야 하므로 메모리를 더 많이 사용함
  - 속도: 좌표를 수집하는 순회(1번) + 최소/최대 찾는 순회(1번)로 로직이 나뉘어 아주 미세하지만 연산이 늘어남
  (이 문제에서는 N이 50이라 차이가 없지만, 데이터가 매우 크다면 비효율적임)

