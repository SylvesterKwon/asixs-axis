---
title: 비트마스크(BitMask) 고급 테크닉
mathjax: false
date: 2020-08-20 00:33:05
tags:
---
## 개요
여기서는 비트마스크를 이용한 문제를 해결할때 사용가능한 몇가지 유용한 고급 테크닉을 소개합니다.
<프로그래밍 대회에서 배우는 알고리즘 문제 해결 전략 (구종만저)> 의 내용을 참고함을 밝힙니다.

## 집합 크기 연산
```cpp
__builtin_popcount(bitset);
```
gcc/g++ 환경에서 켜져있는 비트의 수를 반환합니다. 이 포스트에서 소개되는 내장 명령어는 컴파일러 의존적이기 때문에, 특정환경에서 사용이 불가능할 수 있습니다. 따라서 이를 직접 구현해보면 다음과 같습니다. 
```cpp
int popcount(int bitset){
    if(bitset == 0) return 0;
    return x % 2 + bitcount(x / 2);
}
```
각 비트를 재귀적으로 모두 탐색해준 방법입니다. 빌트인함수를 사용할 수 없을 떄 사용해보세요.

## 최소 원소 탐색
```cpp
__bulitin_ctz(bitset);
```
gcc/g++ 환경에서 켜져있는 최하위 비트의 인덱스를 반환합니다. 이 함수를 사용할 떄, 주의해야할 점은 입력이 0일때는 결과가 정의가 되어있지 않기때문에, 꼭 Bitset이 0인지 확인해야 합니다.

```cpp
int firstbit = (bitset & -bitset);
```
이 방법은 비트의 인덱스가 아닌 해당 비트의 값자체를 반환합니다. 2의 보수의 성질을 이용한 테크닉입니다.

## 최소 원소 삭제
```cpp
bitset &= (bitset - 1);
```
켜져있는 최하위 비트를 삭제하는 테크닉입니다. 이 역시 위에 소개된 비트의 값을 구할 때 사용된 2의 보수의 성질을 이용한 것입니다.

## 참고하면 좋은 사이트들
1. http://graphics.stanford.edu/~seander/bithacks.html