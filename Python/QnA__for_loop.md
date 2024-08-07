# for문 관련
> 1. for 루프 안에서 인덱스 변수 수정 가능 여부
> 2. for-else문
>
## for 루프 안에서 인덱스 변수 수정 가능 여부
Python에서는 `for` 루프 안에서 인덱스 변수를 수정하더라도 루프 제어에는 영향을 미치지 않습니다. 이는 `for` 루프가 시퀀스를 미리 계산하고 해당 시퀀스의 항목을 순차적으로 접근하기 때문입니다. 반면에, C나 Java에서는 `for` 루프의 인덱스 변수를 수정하면 루프 제어에도 영향을 미칠 수 있습니다. 이 점은 두 언어의 루프 구현 방식에서 차이가 발생하기 때문입니다.

### Python
Python의 `for` 루프는 다음과 같이 동작합니다:
```python
for i in range(5):
    for j in range(5):
        i += 2
        print(i, j)
```
위 코드에서 `i`를 수정해도 바깥 루프의 진행에는 영향을 미치지 않습니다. `i`의 변경은 현재 반복에서만 반영되고, 다음 반복에서는 `range` 함수에 의해 다시 초기화됩니다.

### C
C 언어에서는 `for` 루프의 인덱스 변수를 직접 수정하면 루프의 진행에 영향을 줄 수 있습니다:
```c
#include <stdio.h>

int main() {
    int i, j;
    for (i = 0; i < 5; i++) {
        for (j = 0; j < 5; j++) {
            i += 2;
            printf("%d %d\n", i, j);
        }
    }
    return 0;
}
```
위 코드에서 `i += 2`가 실행될 때마다 `i`의 값이 변경되며, 이는 바깥 `for` 루프의 진행에 직접적인 영향을 줍니다. 따라서 예상치 못한 반복이 발생할 수 있습니다.

### Java
Java에서도 C와 유사하게 `for` 루프의 인덱스 변수를 수정할 수 있으며, 이는 루프의 진행에 영향을 줄 수 있습니다:
```java
public class Main {
    public static void main(String[] args) {
        for (int i = 0; i < 5; i++) {
            for (int j = 0; j < 5; j++) {
                i += 2;
                System.out.println(i + " " + j);
            }
        }
    }
}
```
마찬가지로, `i`의 값을 변경하면 바깥 `for` 루프의 인덱스가 수정되어 루프의 진행에 영향을 줍니다.

따라서, Python에서는 `for` 루프 내에서 인덱스 변수를 변경해도 루프 제어에 영향을 주지 않지만, C와 Java에서는 이러한 변경이 루프의 흐름을 바꿀 수 있습니다. 이를 이용해 루프의 흐름을 제어하고자 한다면, Python에서는 `while` 루프를 사용하는 것이 적절합니다.

### Python에서만 안되는 이유
Python에서는 for 루프가 **이터레이터를 사용**하여 동작하기 때문에, 인덱스 변수를 변경해도 루프 제어에 영향을 미치지 않습니다. Python의 for 루프는 리스트나 다른 시퀀스를 반복할 때, 각 항목을 하나씩 가져오는 방식으로 동작합니다. range 함수가 생성하는 이터레이터도 마찬가지입니다.

다른 언어들, 특히 C, C++, Java 등에서는 for 루프가 명시적인 인덱스 변수와 그 조건을 사용하여 루프의 반복을 제어합니다. 인덱스 변수를 직접 변경하면 그 변경이 루프 제어에 직접 영향을 미칩니다.



## for-else문
###### 파이썬 공식 문서 : https://docs.python.org/3/tutorial/controlflow.html#break-and-continue-statements-and-else-clauses-on-loops
### `else` 절
- `for` 또는 `while` 루프도 `else` 절을 가질 수 있다!
- `for` 루프의 `else` 절은 루프가 마지막 반복을 수행한 후 실행된다.
- `while` 루프의 `else` 절은 루프의 조건이 `False`가 된 후 실행된다.
- 루프가 `break` 문에 의해 종료된 경우, `else` 절은 실행되지 않는다.

### 예제: 소수 찾기
```python
for n in range(2, 10):
    for x in range(2, n):
        if n % x == 0:
            print(n, 'equals', x, '*', n // x)
            break
    else:
        # 루프가 끝까지 진행되었을 때만 실행
        print(n, 'is a prime number')
```
###### 지금까지 종료조건 설정하기 힘들었는데 이거 잘 활용하기!!!