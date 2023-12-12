---
layout: default
title: '카드 뭉치'
parent: programmers
grand_parent: coding-test
nav_order: 1
nav_exclude: true
---


[문제링크](https://programmers.co.kr/learn/courses/30/lessons/159994)


```kotlin
class Solution {
    fun solution(cards1: Array<String>, cards2: Array<String>, goal: Array<String>): String {
        var answer : String = "Yes"

        var cards1Idx = 0
        var cards2Idx = 0

        for (str in goal) {

            if(cards1Idx < cards1.size && cards1[cards1Idx] == str) {
                cards1Idx++
            } else if (cards2Idx < cards2.size && cards2[cards2Idx] == str) {
                cards2Idx++
            } else {
                answer = "No"
                break;
            }
        }

        return answer
    }
}
```
## 코틀린 기본 문법 연습
- var : 가변 변수
- val : 불변 변수

