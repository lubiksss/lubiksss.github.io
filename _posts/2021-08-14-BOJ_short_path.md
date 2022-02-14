---
last_modified_at : 2021-08-15
layout : single
title:  "백준 최단경로 알고리즘"
categories: BOJ
tags : [shortpath, python]

toc: true
toc_sticky: true
---
## 서론
<a href='https://www.acmicpc.net/step/26'>단계별로 풀어보기: 최단 경로</a>

이번에 최단경로 찾는 문제들을 많이 풀어보면서 공부한 알고리즘들을 정리해놓으려고 합니다.

## 정리
<table>
  <thead>
    <tr>
        <th style="text-align: center"><strong>구분</strong></th>
        <th style="text-align: center"><strong>BFS,DFS</strong></th>
        <th style="text-align: center"><strong>Dijkstra</strong></th>
        <th style="text-align: center"><strong>Bellman-Ford</strong></th>
        <th style="text-align: center"><strong>Floyd-Warshall</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
        <td rowspan = '2' style="text-align: center">가중치</td>
        <td style="text-align: center">X</td>
        <td style="text-align: center">O</td>
        <td style="text-align: center">O</td>
        <td style="text-align: center">O</td>
    </tr>
    <tr>
        <td style="text-align: center"></td>
        <td style="text-align: center">가중치가 양의 정수일 때만 가능하다.</td>
        <td style="text-align: center">가중치가 음의 정수일 때도 가능하다.</td>
        <td style="text-align: center">가중치가 음의 정수일 때도 가능하다.<br>(단, 음의 사이클이 없어야 한다).</td>
    </tr>
    <tr>
        <td style="text-align: center">구현</td>
        <td style="text-align: center">que, stack 사용</td>
        <td style="text-align: center">heapq 사용</td>
        <td style="text-align: center">DP방식 <br> <strong>distance[n] = min(distance[n], distance[m] + E(m, n))</strong></td>
        <td style="text-align: center">DP방식 <br> <strong>distance[i,j] = min(distance[i,j], distance[i,n] + distance[n,j])</strong> <br>  이차원 배열(행렬) 사용</td>
    </tr>
    <tr>
        <td style="text-align: center">시간 복잡도</td>
        <td style="text-align: center">O(V+E)</td>
        <td style="text-align: center">O(ElogV)</td>
        <td style="text-align: center">O(VE)</td>
        <td style="text-align: center">O(V^3)</td>
    </tr>
    <tr>
        <td style="text-align: center">사용 케이스</td>
        <td style="text-align: center">1:N</td>
        <td style="text-align: center">1:N</td>
        <td style="text-align: center">1:N</td>
        <td style="text-align: center">N:N</td>
    </tr>
  </tbody>
</table>

## 생각
