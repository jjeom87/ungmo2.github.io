---
layout: post
title: Algorithm
categories: Algorithm
---

문제 해결을 위한 논리 또는 수순을 알고리즘(Algorithm : 산법)이라 한다.

문제 해결을 위한 알고리즘은 일반적으로 유일하지 않고 복수 존재한다.

알고리즘은 사람을 위한 알고리즘과 컴퓨터를 위한 알고리즘이 있다. 사람을 위한 알고리즘은 거의 대부분의 경우 컴퓨터를 위한 알고리즘이 아닌 경우가 많다.

예를 들어 225와 105의 최대공약수를 구하기 위하여 사람은 아래와 같은 알고리즘을 사용한다.

![최대공약수](/img/gcd.png)
{: style="max-width:250px; margin: 10px auto;"}

Ans = 5 * 3 = 15

하지만 이 알고리즘을 컴퓨터를 위한 알고리즘으로 변환하는 것은 어렵다. 그 이유는 225와 105의 약수인 5와 3을 인간은 경험적 직감으로 발견한다. 이러한 경험적 직감을 컴퓨터가 이해할 수 있는 논리로 만드는 것은 복잡해지기 때문이다.

최대공약수를 구하는 알고리즘은 [유클리드 호제법](https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C_%ED%98%B8%EC%A0%9C%EB%B2%95)이라는 기계적 방법이 있다.

# 유클리드 호제법

2개의 정수 m, n(m > n)가 있는 경우, m과 n의 최대공약수는 m-n과 n의 최대공약수를 구하는 방법과 유클리드