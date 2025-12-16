## 문제 설명

문자열 s에는 공백으로 구분된 숫자들이 저장되어 있습니다. str에 나타나는 숫자 중 최소값과 최대값을 찾아 이를 "(최소값) (최대값)"형태의 문자열을 반환하는 함수, solution을 완성하세요.
예를들어 s가 "1 2 3 4"라면 "1 4"를 리턴하고, "-1 -2 -3 -4"라면 "-4 -1"을 리턴하면 됩니다.

## 제한 조건

s에는 둘 이상의 정수가 공백으로 구분되어 있습니다.

## 입출력 예
|s|return|
|---|---|
|"1 2 3 4"|"1 4"|
|"-1 -2 -3 -4"|"-4 -1"|
|"-1 -1"|"-1 -1"|

## 풀이 1
<details>
  <summary>펼치기 </summary>

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

string solution(string s) {
  vector<int> numbers;
  string sub="";

  for (int i=0;i<=s.size();i++){
    if ((s[i] == ' ')|(i==s.size())) {
      numbers.push_back(stoi(sub));
      sub="";
      continue;
    }
    sub+=s[i];
  }

  sort(numbers.begin(), numbers.end());
  string answer = to_string(numbers.front()) + " " + to_string(numbers.back());

  return answer;
}
```

</details>

  
## 접근법 및 배운점 1
- 문자열을 숫자로 바꿔 최대, 최소 구하기
- 접근 : 공백 단위로 문자를 저장하여 정수로 변환
  - 반복문 내에서 공백 문자가 나타날 때까지 (또는 배열의 끝) 부분 문자열에 하나의 숫자 문자열로 저장
  - 저장된 정수 벡터를 정렬한 뒤, 처음과 마지막 원소로 return

## 풀이 2
<details>
  <summary>펼치기 </summary>

```cpp
#include <string>
#include <vector>
#include <algorithm> 
#include <sstream>

using namespace std;

string solution(string s) {
    string answer = "";
    
    stringstream ss(s);
    
    int num; 
    vector<int> numbers; 
    
    while (ss >> num) {
        numbers.push_back(num);
    }
    
    sort(numbers.begin(), numbers.end()); // 최소값과 최대값만 필요함에도 전체 정렬을 수행하여 시간복잡도 커짐
    answer = to_string(numbers.front()) + " " + to_string(numbers.back());

    /*
    // 정렬 없이 한 번의 탐색으로 수행, minmax_element는 최솟값과 최댓값의 이터레이터(주소 개념) 쌍(pair)을 반환한다.
    auto result = minmax_element(numbers.begin(), numbers.end());
    
    // 이터레이터이므로 *를 붙여 값을 가져온다.
    // result.first : 최솟값을 가리키는 이터레이터
    // result.second : 최댓값을 가리키는 이터레이터
    answer = to_string(*result.first) + " " + to_string(*result.second);
    */

    return answer;
}
```

</details>

## 접근법 및 배운점 2
- sstream 헤더 활용
  - <sstream> 헤더의 stringstream 객체를 사용하여 긴 문자열을 스트림으로 다룸.
  - ss >> num 구문을 통해 공백(Space)과 줄바꿈(\n)을 자동으로 무시하고, 문자열을 정수(int) 자료형으로 자동 변환하여 추출함.

- 코드 간결성: 풀이 1처럼 인덱스로 직접 접근하거나 공백 검사를 하는 if문 없이도 파싱 로직을 매우 직관적으로 구현 가능.
- 동작 원리: while(ss >> num) 루프는 스트림에서 정수 추출이 성공하는 동안 계속 반복되므로, 입력 개수를 몰라도 안전하게 모든 숫자를 벡터에 담을 수 있음.

- 현재 코드는 최소값과 최대값만 필요함에도 전체 정렬을 수행하고 있다.
정렬 대신 algorithm 헤더의 *min_element()와 *max_element()를 사용하거나,
파싱하면서 min, max 변수를 갱신한다면 정렬 과정을 제거하여 O(N)으로 최적화할 수 있다.
이 방식은 데이터를 모두 정렬할 필요 없이, 리스트를 한 번 훑어서(Scan) 최소/최대만 찾아내므로 효율적이다.
