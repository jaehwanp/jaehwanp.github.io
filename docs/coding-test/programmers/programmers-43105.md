---
layout: default
title: '정수 삼각형'
parent: programmers
grand_parent: coding-test
nav_order: 1
nav_exclude: true
---

[문제링크](https://programmers.co.kr/learn/courses/30/lessons/43105)


1. DFS

```java
class Solution {
	
	int compare = 0;
	
    public int solution(int[][] triangle) {
    	int answer = 0;
    	
        Node node = new Node(0, 0);
        
        dfs(triangle, node, answer);
        
        answer = compare;
        
        return answer;
    }
    
    public void dfs(int[][] triangle, Node node, int answer) {
    	
    	answer += triangle[node.x][node.y];
    	
    	if(node.x+1 < triangle.length) {
    		
    		int sum = answer;
    		
			dfs(triangle, new Node(node.x+1,node.y), sum);
			dfs(triangle, new Node(node.x+1,node.y+1), sum);
			
    	}
    	
    	if(node.x+1 == triangle.length) {
    		if(compare < answer) {
    			compare = answer;
    		}
    	}
			
	}
    
}

class Node {
	
	int x;
	int y;
	
	public Node(int x, int y) {
		this.x = x;
		this.y = y;
	}
	
}
```
**O(n*2)**  

문제의 조건에서 `최대 깊이 500`을 고려 하지 못한방법

최악의 경우 500²번 실행해야하기에 효율성이 떨어짐 

---  

2. 최적화  

```java
class Solution {
	public int solution(int[][] triangle) {
    	int answer = 0;
    	
    	for(int i=0; i<triangle.length-1; i++) {
    		for(int j=0; j<triangle[i].length; j++) {
    			
    			if(j==triangle[i].length-1) {
    				triangle[i+1][j+1] += triangle[i][j];
    				if(i==0 && j==0) {
    					triangle[i+1][j] += triangle[i][j];
        			}
    			} else {
    				
    				if(j==0) {
        				triangle[i+1][j] += triangle[i][j];
        			}
    				
    				if(triangle[i][j] > triangle[i][j+1]) {
    					triangle[i+1][j+1] += triangle[i][j];
    				} else {
    					triangle[i+1][j+1] += triangle[i][j+1];
    				}
    			}
    		}
    	}
    	
    	Arrays.sort(triangle[triangle.length-1]);
    	
    	answer = triangle[triangle.length-1][triangle.length-1];
    	
        return answer;
    }
}
```

**O(n)**  

모든 노드를 한 번만 방문하므로 효율성에서 좋아짐

---  
# 

- 만약 1~99999999 까지 더한다면  

```java
for(int i=1; i<=99999999; i++) {
	answer += i;  // O(n)
} 
```
단순하게 위 식으로 쓰기보단, 생각하고 효율적인 방식을 결정해야함

```java
answer = 99999999 * (1+99999999) / 2 // O(1)
```
위 식처럼.