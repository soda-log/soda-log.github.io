---
layout: post
title: "프로그래머스 점찍기 문제"
date: 2026-01-01 00:00:00 +0900
categories: [Algorithm, Troubleshooting]
tags: [Kotlin]
math: true
---
https://school.programmers.co.kr/learn/courses/30/lessons/140107

Lv. 2. 내가 풀었을 때의 정답률: 42%

## 문제 해석
원점과의 거리가 d를 넘지 않는 점 $x$, $y$의 위치를 구해야 한다.  
이 때, $x=a*k (a = 0, 1, 2, 3...)$, $y=b*k (b = 0, 1, 2, 3...)$ 이다.  
여기서 $k$ 와 $d$ 가 주어졌을 때, 점이 총 몇 개 찍히는지 구하는 문제이다.

## 코드
₩₩₩

class Solution {
    fun solution(k: Int, d: Int): Long {
        var answer: Long = 0
        
        if (k == 0) {
            return 0
        }
        
        for (i in 0..d / k) {
            val x = k * i
            val doubleD = d.toDouble()
            val doubleX = x.toDouble()
            val maxY = (Math.sqrt(doubleD * doubleD - doubleX * doubleX)).toInt()
            // println("$x, $maxY")
            answer += (maxY / k + 1)
        }
        return answer
    }
}

₩₩₩

## 문제 풀이
원의 공식인 $x^2+y^2=d^2$ 를 이용한다.  
x의 최대값은 y가 0일 때인 d 이고, k 가 주어지기 때문에 a의 최대값은 d/k 이다.  
a가 0부터 d/k 까지 for문을 돌면서 가능한 y의 개수를 구하면 되는데, x 값이 정해져 있다면, y의 최대값은 $sqrt(d^2 - x^2)$ 이다.  
y의 개수는 0부터 최대값의 자연수이므로, ₩sqrt(d*d-x*x).toInt()+1₩ 이다.

## TroubleShooting
1. k, d 가 1,000,000 값까지 가질 수 있기 때문에 int 로 계산하면 overflow 가 발생한다. double 로 계산하는 것이 바람직하다.
2. sqrt 함수를 쓰려면 ₩Math.sqrt()₩ 로 사용해야 한다.