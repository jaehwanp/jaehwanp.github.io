---
layout: default
title: '마법의 엘레베이터'
parent: programmers
grand_parent: coding-test
nav_order: 1
nav_exclude: true
---


[문제링크](https://programmers.co.kr/learn/courses/30/lessons/148653)


```java
import java.util.*;

class Solution {
	
    public int solution(int storey) {

		int answer = pressBtn(storey, 10, 0);
		
		return answer;
	}


	public int pressBtn(int storey, int compare, int total) {

		int mod = storey % compare;

        int digit = compare / 10;

        if (storey == 0) {

        } else if (mod < 5*digit || (mod == 5*digit && (storey % (compare*10) < 5 * compare))) {
            storey -= mod;
            total += mod / digit + qq(storey, compare*10, total);
        } else if (mod > 5*digit || (mod == 5*digit && (storey % (compare*10) >= 5 * compare))) {
            storey += compare - mod;
            total += (compare - mod) / digit + qq(storey, compare*10, total);
        }

        return total;

	}
}
 
```

---

# 재귀함수




1의 자리부터 올라가면서 생각한다.

1의 자리가 `6` 이상이면 `10`을 만들어 올리는게 이득이다.
- `6`을 `0`으로 내리면 6 필요 -> 총합 6
- `6`을 `10`으로 올리면 4 필요
	- 다시 `10`을 `0`으로 만드려면 1필요 -> 총합 5

1의 자리가 `4` 이하면 `0`을 만들어 내리는게 이득이다.
- `4`를 `0`으로 내리면 4 필요 -> 총합 4
- `4`를 `10`으로 올리면 6 필요
	- 다시 `10`을 `0`으로 만드려면 1필요 -> 총합 7

하지만,

1의 자리가 `5`라면 올릴지 말지 고민해야한다.
- 10의 자리 + 1의 자리가 `55` 이상일 때,
	- 1의 자리를 올리면 : `55` - 5 - `60` - 4 - `100` - 1 - `0` => 총합 10
	- 1의 자리를 내리면 : `55` - 5 - `50` - 5 - `0` => 총합 10
- 10의 자리 + 1의 자리가 `55` 미만일 때
	- 1의 자리를 올리면 : `45` - 5 - `50` - 5 - `0` => 총합 10
	- 1의 자리를 내리면 : `45` - 5 - `40` - 4 - `0` => 총합 9

따라서 `55` 이상이면 올리고 미만이면 내린다.

예를들어 storey 가 `1234567` 이라면
1. `67` 은 `55` 이상이니까 올린다 => `70` -> `1234570`
2. `57` 은 `55` 이상이니까 올린다 => `60` -> `1234600`
3. `46` 은 `55` 미만이니까 내린다 => `40` -> `1234000`
4. `34` 은 `55` 미만이니까 내린다 => `30` -> `1230000`
5. `23` 은 `55` 미만이니까 내린다 => `20` -> `1200000`
6. `12` 은 `55` 미만이니까 내린다 => `10` -> `1000000`
6. `01` 은 `55` 미만이니까 내린다 => `0` -> `0`

위에서 올리고 내린 개수만큼 `total`에 더하면 된다.

