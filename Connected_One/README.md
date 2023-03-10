# Connected_One
2차원 matrix인 canvas에서 1을 찾은 후 연결된 1을 같은 숫자로 변경하는 프로그램
응용 : 코딩테스트 무인도

## Python file
FILL.py
재귀함수를 사용하여 구현

FILL_Comment.py
주석 첨부

NRFILL.py
재귀함수를 사용하지 않고 stack을 사용하여 구현

NRFILL_Comment.py
주석 첨부

## Algorithm
![picture1](https://user-images.githubusercontent.com/123911778/216236471-9fe8dce0-3662-4315-95da-77a307ff7c7e.png)

0과 1이 채워져 있는 2차원 배열에서 서로 연결되어 있는 1을 다른 숫자로 채워넣는 프로그램이다.
[picture1]에서 위의 matrix을 넣고 프로그램을 돌리면 아래 matrix을 출력한다.
상하좌우로 연결되어 있는 1의 집합은 총 4개가 나오고 각각 2, 3, 4, 5로 변경된 것을 볼 수 있다.

- 행렬에서 1의 위치를 찾는다.
- 1이 있는 좌표를 기준으로 8가지 방향에 있는 좌표에 있는 숫자가 1인지 확인한다.
- 1이 있으면 같은 숫자로 채운다.
- 연결되어 있다는 것은 1번 좌표에서 오른쪽 위로 간 다음 거기서 다시 8가지 방향을 확인하고 다시 이동한 다음 확인하는 식으로
- 재귀함수와 stack을 사용하여 구현할 수 있다.

![picture2](https://user-images.githubusercontent.com/123911778/216238271-ed7f94c6-46fe-4a0d-ba5d-99547d3a1b22.png)
- matrix에서 1을 찾는다.
- 8가지 방향에 대해서 1이 있는지 확인한다.
- 1이 아니라면 다른 방향을 살핀다.
- 1이 있다면 현재 좌표를 stack에 저장한 후 1이 있는 위치로 이동하고 8가지 방향에서 1이 있는지 확인한다.

![picture3](https://user-images.githubusercontent.com/123911778/216238274-6b8ffe74-69f1-42df-8d24-926edb64584a.png)

첫 번째 1의 모임은 위의 방향으로 이동하면서 2로 바뀌게 된다.

### 재귀함수
컴퓨터는 기본적으로 stack의 구조를 가지고 있기 때문에 재귀함수를 사용하는 것으로 stack을 사용한 것과 같은 효과를 얻을 수 있다.
FILL(x, y, cnt) 함수를 호출하면 FILL 내부에 FILL(x, y-1, cnt), FILL(x+1, y, cnt), FILL(x, y+1, cnt), FILL(x-1, y, cnt)가 호출되고
이것은 x, y, cnt을 실행하면서 x, y-1, cnt / x+1, y, cnt / x, y+1, cnt / x-1, y, cnt을 각각 stack에 push한 것과 같다.

재귀함수는 함수에서 함수를 호출하는 것으로 함수에서 빠져나오기 위해 종료조건을 두어야 한다.
함수를 끝낼 수 있는 return이 들어가 있어야 하고(출력을 위한 것이라면 return이 없을 수 있다.) 함수를 호출하는 범위가 줄어들어야 한다.

여기서는 matrix가 1인 경우에만 재귀함수를 호출하고 아니면 return을 하는 식으로 함수를 끝낼 수 있는 조건이 붙어 있고
내부에서 호출하는 함수는 8가지 방향의 좌표를 사용한 것으로 matrix를 모두 탐색하면 함수가 종료된다.

재귀함수를 생성할 때는 
1. 결과를 향한 방향 (정방향/역방향)
2. 반환값 (있음/없음)
3. 종료조건
을 고려해보자.

### Stack
스택은 후입선출(LIFO, Last In First Out)의 특징을 가진 자료구조이다.
push(data) 스택에 data을 삽입하는 함수
pop() 스택의 맨 위에 있는 데이터를 꺼내는 함수 (스택에서 데이터는 삭제)
size() 스택의 길이를 출력하는 함수
Empty() 스택이 비어있는지 확인하는 함수
top() 스택의 가장 위 index을 출력하는 함수

CodingTest을 보면 stack을 활용한 문제가 많이 있고 특히 반복문 대신 stack을 사용하여 시간을 줄이는 경우가 다수 존재한다.

## 프로그래머스 무인도 여행
![picture4](https://user-images.githubusercontent.com/123911778/216235844-0aac594b-b989-4f5f-b943-84b4034ab873.png)
![picture5](https://user-images.githubusercontent.com/123911778/216235850-5b5a72f6-282c-4472-9b38-bbeee914a821.png)

picture4와 같이 바다는 X, 숫자는 무인도에서 생활할 수 있는 식량의 양이 나와있다.
상하좌우로 연결된 숫자는 하나의 무인도라고 가정하고 떨어져 있거나 대각선에 있는 곳은 다른 무인도라고 가정한다.
각각의 무인도에서 생활할 수 있는 날짜를 반환하는 문제이다.

picture4에서 연결된 무인도는 총 3개인 것을 알 수 있다.
각각의 무인도마다 생활할 수 있는 날짜는 picture5와 같다.

입력된 matrix에서 연결된 무인도를 찾고 연결된 무인도의 식량을 더하는 문제에서 이번 알고리즘을 사용했다.
FILL.py와 NRFILL.py에서는 상하좌우 대각선에서 8가지 방향을 연결된 것으로 보았으나
이번 문제에서는 상하좌우에서만 연결된 것으로 판단한다.

입력된 문자열에 대해서 'X'이면 0, '1' ~ '9'사이의 문자면 1을 저장한 2차원 matrix을 제작한 후
NRFILL.py의 알고리즘을 사용하여 각각의 무인도의 1을 2, 3, 4로 변환한다.
이후 2, 3, 4로 저장된 좌표에 대해서 각각 무인도의 식량을 더하면 하나의 무인도에서 생활할 수 있는 날짜를 구할 수 있다.
