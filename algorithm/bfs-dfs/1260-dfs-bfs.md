# 백준 1260 DFS와 BFS

## 1. 문제 

![https://www.acmicpc.net/problem/1260](../../.gitbook/assets/image%20%28398%29.png)

{% embed url="https://www.acmicpc.net/problem/1260" %}



## 2. 소스 코드 

```python
# DFS 함수 생성
def dfs(V, myList, visited):
    if visited[V] == 0:                   #만약 방문하지 않았다면
        visited[V] = 1                    #방문하고
        result.append(V)                  #방문 순서 저장하고
        for node in myList[V]:            #방문한 정점들에 대해 같은 과정 실행
            dfs(node, myList, visited)
    return(result)


# BFS 함수 생성
def bfs(V, myList, visited):
    que = []                              #que 생성
    que.append(V)                         #시작 정점 que에 추가
    while que:                            #que에 값이 존재하는 동안 다음을 실행
        now = que.pop(0)                  #que에서 처음 값을 뽑아서 now에 할당
        if visited[now] == 0:             #now 정점을 방문한 적이 없다면
            visited[now] = 1              #now 정점을 방문하고 
            result.append(now)            #now 정점을 결과에 저장
            for node in myList[now]:      #now와 연결된 정점들을 que에 추가 
                que.append(node)
    return(result)    
 
 
# 입력 받기 
N, M, V = map(int, input().split())
myList = [[] for _ in range (N+1)]        #정점 연결 정보를 저장할 리스트 생성 


# 정점 연결 정보 myList 저장 
for _ in range(M):
    a, b = map(int, input().split())  
    myList[a].append(b)                   #양방향 연결이기 때문에 양쪽에 저장
    myList[b].append(a)
for _ in myList:
    _.sort()


# 방문한 정점 및 방문한 정점 순서 저장 리스트 생성
visited = [ 0 for _ in range(N+1) ]
result = []


# DFS 결과 출력
dfs = dfs(V,myList,visited)
for i in dfs:
    print (i, end=' ')                      #end=''하면 한 줄에 이어서 출
print('')


# BFS 결과 출력
visited = [ 0 for _ in range(N+1) ]         #visited, result는 reset 필수!
result = []
bfs = bfs(V,myList,visited)
for k in bfs:
    print (k, end=' ')
```

