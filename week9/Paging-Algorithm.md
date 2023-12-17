페이징 기법을 사용할 때 OS는 주기억장치에 필요한 페이지가 없을 때 어떤 페이지 프레임을 선택해서 교체할지 결정하는데, 그 방법을 페이지 교체 알고리즘이라고 한다.

# OPT (Optimal)

![](https://velog.velcdn.com/images/urjimyu/post/4a85cd40-8378-4809-b832-2dd396e71f2b/image.png)

- 가장 오랫동안 사용되지 않을 페이지 교체
- 가장 이상적이지만 앞으로 어떤 페이지가 사용될지 미리 아는 것은 불가능하다.

# FIFO (First In First Out)

![](https://velog.velcdn.com/images/urjimyu/post/41008c90-c150-486f-a010-e4e998b85676/image.png)

- 선입선출
- 메모리에 제일 먼저 올라온 페이지 먼저 내보내기
- 간단하다
- Belady's Anomaly => 실제로 선입선출이 되지 않는 경우가 생길 수 있다.
  ![](https://velog.velcdn.com/images/urjimyu/post/460239a1-562c-46b4-8b8c-a4e0ef43c446/image.png)

# LRU (Least Recently Used)

- 가장 오랫동안 사용되지 않은 페이지 교체
- 가장 오랫동안 사용하지 않은 페이지는 앞으로도 사용할 확률이 적다는 아이디어
- 즉, 시간 지역성(최근 참조된 페이지가 가까운 미래에 다시 참조될 가능성 높은 성질) 고려
- 큐를 활용해서 사용한 데이터를 맨 위로 올리는 형식으로 구현

# LFU (Least Frequently Used)

- 참조 횟수가 가장 작은 페이지 교체
- LRU는 직전 참조된 시점만 반영, LFU는 전체 참조 횟수를 통해 고려
- 제일 최근 불러온 페이지가 교체될 수 있는 단점

# MFU (Most Frequently Used)

- 참조 횟수가 가장 많은 페이지 교체
- 가장 많이 사용된 페이지는 앞으로는 더 사용되지 않을 것이라는 아이디어

# NUR (Not Used Recently), 클럭 알고리즘

- 최근에 사용하지 않은 페이지 교체
- 교체되는 페이지의 참조 시점이 가장 오래되었다는 것을 보장하진 못한다.
- 각 페이지마다 두 개의 비트(참조 비트와 변형 비트)가 사용됨
- 우선순위는 참조비트가 변형비트보다 높다.

---

### References

[페이지 교체 알고리즘](https://doh-an.tistory.com/28)
