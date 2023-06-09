---
layout: default
title: '등굣길'
parent: programmers
grand_parent: coding-test
nav_order: 1
nav_exclude: true
---

[문제링크](https://programmers.co.kr/learn/courses/30/lessons/42898)


```java
import java.util.*;

class Solution {
	
    public int solution(int[][] maps) {
    	
        int answer = 0;
        boolean meet = false;
        boolean[][] visited = new boolean[5][5];
        Queue<Node> q = new LinkedList<Node>();
        
        int[] dy = {0,1,-1,0};
        int[] dx = {-1,0,0,1};
    	
    	int cy = 0, cx = 0, cd = 1;
    	
    	// 처음 0,0 시작
    	Node node = new Node(cy,cx,cd);
    	visited[cy][cx] = true;
    	q.offer(node);
    	
    	while(!q.isEmpty()) {
    		
    		Node nd = q.poll();
    		cd = nd.distance + 1;
    		
    		for(int i=0; i<4; i++) {
    			
    			cy = nd.y + dy[i];
    			cx = nd.x + dx[i];
    			
    			if(cy >= 0 && cx >= 0 && cy <= 4 && cx <= 4) {
    				if(maps[cy][cx] == 1 && !visited[cy][cx]) {
    					
	    				visited[cy][cx] = true;
	       				q.offer(new Node(cy, cx, cd));
	       				
	       				if(cy == 4 && cx == 4) {
	       					answer = cd;
	       					meet = true;
	       				}
    				}
    			}
    		}
    	}
    	
    	if(meet) {
    		return answer;
    	} else {
    		return -1;
    	}
    }
    
}

class Node {
	int y;
	int x;
	int distance;
	
	public Node(int y, int x, int distance) {
		this.y = y;
		this.x = x;
		this.distance = distance;
	}
	
}
```

---

## bfs (너비 탐색 기법)

#### 이 문제에서 너비 탐색 기법을 쓴 이유

- 많은 노드와 루트가 있지 않다면 bfs는 최단거리를 구하는데 용이함


#### dfs 언제씀?

- 보통 순열, 조합 문제에서 용이함.
