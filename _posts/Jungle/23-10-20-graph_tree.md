---
layout: single
title: Graph & Tree
categories: Jungle
---

## 그래프
* 단순히 노드(N, Node)와 그 노드를 연결하는 간선(E, Edge)를 하나로 모아놓은 자료구조
* 그래프는 여러개의 고립된 부분으로 구성될 수 있음

### 용어
* 정점(vertex): 위치라는 개념(Node와 같은 개념)
* 간선(edge): 노드간 연결 선
* 인접 정점(adjacent vertex): 간선에 의해 직접 연결된 정점
* 정점의 차수(degree): 무방향 그래프에서 하나의 정점에 인접한 정점의 수
* 아크(arc): 방향성 엣지, 엣지에 방향성이 부여되면 아크가 됨(= arrows)

### 그래프 종류
* 무방향, 양방향 그래프: 간선을 통한 이동이 한 방향, 양 방향으로 구분
* 가중치 그래프: 엣지에 비용이나 가중치가 할당된 그래프
* 연결, 비연결 그래프: 무방향 그래프에서 모든 정점쌍에 항상 경로가 있는 경우(트리), 없는 경우로 구분
* 사이클, 비순환 그래프
* 완전 그래프: 모든 정점이 연결된 그래프

### 그래프의 구현
1. 인접 리스트
    * 장점
        * 정점들의 연결 정보 탐색에 O(n)의 시간복잡도
        * 인접 행렬보다 공간의 낭비가 적음
    * 단점
        * 연결 정보 확인이 인접 행렬보다 오래걸림
        * 구현이 인접 행렬보다 어려움
2. 인접 행렬
    * 장점
        * 정점들의 연결 정보 탐색에 O(1)의 시간복잡도
        * 구현이 쉬움
    * 단점
        * 생성 시 O(n^2)의 시간복잡도
        * 항상 2차원 배열 필요

## 트리
주요 속성: 루트 노드를 제외한 모든 노드는 단 하나의 부모 노드를 갖는다.

### 용어
* root node: 트리의 가장 위에 있는 노드
* parent node: 어떠한 노드 a에 대하여 해당 노드를 가리키는 상위 노드
* child node: 어떠한 노드 b에 대하여 해당 노드가 가리키는 하위 노드
* depth: 트리의 깊이, 각 층은 level이라 칭함
* leaf node: 각 트리의 말단 노드

## 이진 트리
자식 노드가 최대 두 개인 노드로 구성된 트리

### 종류
* 정이진트리(full binary tree)
* 완전이진트리(complete binary tree)
* 균형이진트리(balanced binary tree)

### 정, 완전 이진 트리는 1차원 배열로 표현 가능
```
left_child_index = 2 * parent_index + 1
right_child_index = 2 * parent_index + 2
```

## 트리 순회
각 노드를 체계적인 방법으로 방문하는 과정
* 전위 순회(pre-order): root - left subtree - right subtree
* 중위 순회(in-order): left subtree - root - right subtree
* 후위 순회(post-order): left subtree - right subtree - root

## 스패닝 트리(신장 트리, Spaning tree)
* 그래프의 최소 연결 부분 그래프
    * 여기서 최소 연결이란 간선의 수가 가장 적음을 의미
* n개의 정점을 갖는 그래프의 최소 간선의 수는 n-1개이고, n-1개의 간선으로 연결되어 있으면 필연적으로 트리 형태가 되고, 이것이 신장 트리가 됨
* 즉, 그래프에서 일부 간선을 선택해서 만든 트리

### 특징
* DFS, BFS를 사용해서 싱장 트리를 찾을 수 있음
    * 탐색 도중에 사용된 간선만 모으면 가능
* 하나의 그래프에는 많은 신장 트리가 존재 가능
* 모든 정점들이 연결되어있어야 하고, 사이클을 포함해서는 안됨
* n개의 정점을 n-1개의 간선으로 연결해야 함

## MST(Minimum Spaning Tree, 최소 신장 트리)
Spaning tree중에서 사용된 가중치의 합이 최소인 트리

### 특징
* 간선의 가중치의 합이 최소여야 함
* n개의 정점을 갖는 그래프에 대해 반드시 n-1개의 간선만을 활용해야 함
* 사이클이 포함되어서는 안됨

### 구현 방법
1. Kruskal MST Algorithm
2. Prim MST Algorithm

## Kruskal MST
1. 그래프의 모든 간선들을 가중치의 오름차순으로 정렬
2. 정렬된 간선 리스트에서 순서대로 사이클을 형성하지 않는 간선을 선택
    * 즉, 가장 낮은 가중치를 먼저 선택
    * 사이클을 형성하는 간선은 제외

## Prim MST
* 시작 정점에서 출발하여 신장트리 집합을 단계적으로 확장해 나가는 방법
    * 정점 선택을 기반으로 하는 알고리즘
    * 이전 단계에서 만들어진 신장트리를 확장하는 방법

1. 시작단계에서는 시작 정점만이 MST 집합에 포함됨
2. 앞 단계에서 만들어진 MST집합에 인접한 정점들 중에서 최소 간선으로 연결된 정점을 선택하여 트리를 확장
3. 위의 과정을 트리가 n-1개의 간선을 가질 때 까지 반복