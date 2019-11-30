---
layout: post
cover: 'assets/images/cover7.jpg'
navigation: True
title: 테스트
date: 2019-11-04 01:01:28
tags: fables fiction
subclass: 'post tag-test tag-content'
logo: 'assets/images/logo.png'
author: parkhyuseo
categories: 알고리즘
---

# 프로그래머스 Level 2 - 카펫


## 알고리즘

완전탐색

### **문제 설명**

Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 빨간색으로 칠해져 있고 모서리는 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.

![](https://grepp-programmers.s3.amazonaws.com/files/ybm/7c94563a35/2ff27ac9-97d0-43a9-9cf8-a344b8e7912e.png)

Leo는 집으로 돌아와서 아까 본 카펫의 빨간색과 갈색으로 색칠된 격자의 개수는 기억했지만, 전체 카펫의 크기는 기억하지 못했습니다.

Leo가 본 카펫에서 갈색 격자의 수 brown, 빨간색 격자의 수 red가 매개변수로 주어질 때 카펫의 가로, 세로 크기를 순서대로 배열에 담아 return 하도록 solution 함수를 작성해주세요.

### 제한사항

-   갈색 격자의 수 brown은 8 이상 5,000 이하인 자연수입니다.
-   빨간색 격자의 수 red는 1 이상 2,000,000 이하인 자연수입니다.
-   카펫의 가로 길이는 세로 길이와 같거나, 세로 길이보다 깁니다.


##   풀이

3개로 나눠서 경우의 수를 구할 수 있다. Red의 Width, Height 그리고 Brown의 Width, Height 마지막으로 Total(Red+Brown)의 Width, Height 이 3가지가 모두 맞아 떨어지면 된다.

그래서 루프를 돌며 Total개수로 직사각형을 만들 수 있는 경우의 수와 Red개수로 직사각형으로 만들 수 있는 경우의 수 2개를 인풋으로 가지고 직사각형을 만들 수 있는지 검사하는 함수를 만들어 가능할경우 Total의 Width, Height를 출력했다.

시간은 고려 안하고 짰는데 아래 2가지 방식으로 시간을 줄일 수 있을 것 같다.

1.  가로길이는 세로길이보다 같거나 길다.(For문을 중간까지만 돌아도 된다)
2.  for문을 미리 다 돌아놓고 조합을 구한다음에 경우의 수를 구하면 조금이라도 연산량이 줄어든다.

-   다른 사람의 문제 풀이에서 For문 하나로 푼걸 봤는데, 테두리(브라운)의 두께가 1인걸로 산정하고 푼 식이었다. 아마 테스트케이스가 두께가 1인게 전부라서 통과가 된 것 같다.

## 코드
```python
def is_possible(total_width, total_height, red_width, red_height) -> bool:
    if total_width - 2 < red_width or total_height - 2 < red_height :
        return False

    return True

def solution(brown, red):
    answer = []

    total = brown+red
    for i in range(1, total+1):
        if total % i != 0:
            continue

        total_height, total_width = i, total // i
        for j in range(1, red+1):
            if red % j != 0:
                continue

            red_height, red_width = j, red // j
            #print("{0}, {1} : {2}, {3}".format(total_width, total_height, red_width, red_height))
            if is_possible(total_width, total_height, red_width, red_height):
                return [total_width, total_height]


    return answer
```