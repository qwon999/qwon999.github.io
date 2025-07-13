---
title: "[백준 1654] 랜선 자르기 (Java) - int 자료형으로 오버플로우 다루기"
date: 2025-07-13 18:55:00 +0900
categories: [Algorithm]
tags: [백준, 이분탐색, 오버플로우, 정수, 자료형]
---

## 문제 링크

[https://www.acmicpc.net/problem/1654](https://www.acmicpc.net/problem/1654)

## 핵심 아이디어: 이분 탐색
N개의 랜선을 만들 수 있는 랜선의 최대길이를 찾는 문제입니다. 클래식한 이분 탐색 문제입니다. min=1 max=2^31-1로 초기화 하고, mid값을 갱신해가면 됩니다.

## long을 쓰지 않고 싶다.
대부분의 풀이가 오버플로우 때문에 long자료형을 사용합니다. 하지만, 문제에서 이러한 말이 써있습니다.

> 랜선의 길이는 2^31-1보다 작거나 같은 자연수이다.


따라서 정답은 최대 2^31-1이겠죠. 이는 int자료형이 가질 수 있는 최댓값이기도 합니다.

하지만, 이로 인해 이분탐색에서의 문제가 발생합니다.
```java
while(min <= max){
    int mid = min + (max - min) / 2;
    
    int cnt = 0;
    // 랜선들을 mid로 나눠서 갯수를 더해줌
    for(int a : arr){
        cnt += a / mid;
    }

    if(cnt < n){ // 갯수가 n보다 작다면 mid값이 작아져야 합니다.
        max = mid - 1;
    } else { /// 갯수가 n이상이라면 mid값이 커져도 됩니다.
        min = mid + 1;
    }
}

```

이런식으로 코드를 작성하고 시간초과 판정을 받는 경우가 많습니다.

이로인해 다들 long자료형으로 바꿉니다.
하지만, 문제가 어디서 발생하는 지 조금만 생각해본다면, int자료형으로 해결할 수 있을 것 같습니다.

왜 시간초과가 발생했을까요?
바로 정답이 2^31-1일 때 입니다.

시간초과가 발생하는 분들은 코드에 해당 테스트케이스를 넣어보세요.
```
3 3
2147483647
2147483647
2147483647
```
정답이 2147483647이 나와야하겠죠?
하지만, 무한루프에 빠지게 됩니다.

여기서 오버플로우 문제를 마주하게되는 것입니다.

```java
while(min <= max)
```
min값이 max보다 작거나 같을 동안 루프는 계속 됩니다.
즉, min값이 max보다 커짐으로써 루프를 탈출합니다.

하지만, 위의 상황에서 mid=2147483647일 때,
```java
else { /// 갯수가 n이상이라면 mid값이 커져도 됩니다.
        min = mid + 1;
    }
```
해당 코드를 만나게 되고 min 값은 2147483647 + 1이됩니다.
따라서 2147483648이 되고 코드가 끝이 나야하는데, int형의 오버플로우로 인해서 -2147483648이 됩니다.(왜 -2147483648이 되는 지는 다음번에 비트연산과 함께 다루도록 하겠습니다.)
이렇게 되면 min <= max 조건이 계속해서 만족되고 코드가 무한루프에 빠지는 것이죠.

그렇다면 어떻게 해결할 수 있을까요? 간단합니다. 그냥 min이 음수가 되면 루프를 강제로 끝내면 됩니다.
```java
while(min <= max){
    int mid = min + (max - min) / 2;
    int cnt = 0;
    for(int a : arr){
        cnt += a / mid;
    }
    if(cnt < n){
        max = mid - 1;
    } else {
        min = mid + 1;
        // min이 음수가 되면 정답 출력하고 코드 끝냄.
        if(min < 0){
            System.out.println(Integer.MAX_VALUE);
            return;
        }
    }
}
```

이렇게 되면 long 자료형을 쓰지 않고 문제를 풀 수 있습니다.

## 전체코드
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

class Main {

    private static int readInt() throws Exception {
        int val = 0;
        int c = System.in.read();
        while (c <= ' ') {
            c = System.in.read();
        }
        do {
            val = 10 * val + c - 48;
        } while ((c = System.in.read()) >= 48 && c <= 57);
        return val;
    }

    public static void main(String[] args) throws Exception {
        int k = readInt();
        int n = readInt();
        int arr[] = new int[k];
        int max = Integer.MAX_VALUE;
        int min = 1;
        for (int i = 0; i < k; i++) {
            arr[i] = readInt();
        }
        while(min<=max){

            int mid = min+(max-min)/2;
            int cnt = 0;
            for(int a : arr){
                cnt += a/mid;
            }
            if(cnt<n){
                max = mid-1;
            }else{
                min = mid+1;
                if(min<0){
                    System.out.println(Integer.MAX_VALUE);
                    return;
                }
            }
        }
        System.out.println(min-1);
    }
}
```
저는 int자료형을 사용하고 빠른 입출력을 사용함으로써 java기준 1등을 달성할 수 있었습니다.

![1등 달성 인증](assets/img/bj1654.png)

궁금증이 있으신 분들은 편하게 댓글 남겨주세요.







