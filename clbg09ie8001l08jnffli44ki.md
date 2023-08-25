---
title: "BFS and DFS Beginners Overview in c++"
seoTitle: "Competitive Programming - DFS and BFS Overview for beginners in c++"
seoDescription: "In this post you will learn how to solve basic to intermediate competitive programming problems using Breath-first-search (BFS) and Depth-first-search (DFS)"
datePublished: Fri Dec 09 2022 04:25:54 GMT+0000 (Coordinated Universal Time)
cuid: clbg09ie8001l08jnffli44ki
slug: bfs-and-dfs-beginners-overview-in-c
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1670695542429/me-naCOvJ.png
tags: cpp, algorithms, data-structures, competitive-programming, beginnersguide

---

## Introduction

Hello everyone! 👋, In this Post, we'll dive deeper into Graphs in programming, we'll take a look at the most common algorithms for solving competitive programming problems using Graphs, DFS, and BFS, and how to implement them in c++ while we solve some interesting problems.

If you have no idea what a graph is and how to represent one check out my previous post: [Graphs Introduction For Beginners](https://blog.garybricks.com/graphs-introduction-for-beginners#heading-introduction)

## Depth-first search (DFS)

Depth-first search is a straightforward graph traversal technique. The idea is that the algorithm begins at a specified node and from there proceeds to visit all nodes that are reachable from the current node. This algorithm always follows a single path in the graph as long as it finds new **unvisited** nodes. If the algorithm has no new unvisited nodes it returns to previous nodes and begins to explore in other directions. With DFS, each node is visited only once.

### DFS visualization

Let's see how a DFS algorithm would process the following graph:

![DFSanimation.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1666385057024/hfQKW8FrE.gif align="left")

In this case, we are starting from node 1, and the algorithm proceeds to visit the neighbor node 2, the process repeats for nodes 3 and 4 until node 5 where there are no longer new **unvisited** nodes, that's the moment our algorithm returns to node 4 and chooses another route, in this case, node 6. Once the algorithm reaches node 6 there are no longer new unvisited nodes so the search terminates. The time complexity of DFS is `O(n+m)` where **n** is the number of nodes and **m** is the number of edges.

### Implementation

DFS can be very easy and convenient to implement using recursion, the main idea is that you define a function that receives the current node and marks it as visited, then checks for all of the adjacent nodes to that node and sends the same function with those nodes as long as they are not visited.

```cpp
#include <iostream>
#include <vector>
using namespace std;

int n, k;
vector<vector<int>> GRAPH;
vector<bool> visited;

void DFS(int current) {
  visited[current] = 1; // marking the active node as visited
  cout << "currently on:" << current << endl;
  for (auto node : GRAPH[current]) // iterate through all of it's neighboors 
    if (!visited[node]) DFS(node); // send DFS if it's a new node
}

int main() {
  cin >> n >> k;
  GRAPH.resize(n + 1);
  visited.resize(n + 1);
  for (int i = 0; i < k; i++) {
    int a, b;
    cin >> a >> b;
    GRAPH[a].push_back(b);
    GRAPH[b].push_back(a);
  }

  DFS(1); // starting algorithm from node 1
  return 0;
}
```

In the code cell above you can see the implementation using an adjacency list to represent the graph and a simple vector of booleans to keep track of the visited nodes. In this case, we are sending the DFS algorithm starting from node 1 but you can try and make the algorithm start from a different node to see what the output is.

## Breadth-first search (BFS)

Breadth-first search is also a traversal algorithm that is very commonly used for searching a node, finding the shortest path in a graph, and for simulations. BFS visits all the nodes but in increasing order based on their distance from the starting node, because of this, BFS can help us calculate the distance from the starting node to all other nodes.

### BFS visualization

Let's see what a BFS algorithm would look like on our example graph.

![BFSanimation.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1666460750679/xH2mEGQ2E.gif align="left")

Just like a DFS, BFS starts from a specified node, and from there visits **ALL** of the nodes that are exactly 1 node away, once all nodes of that level are visited, the algorithm continues with the second level and this process continues until all levels are visited.

The time complexity of BFS is `O(n+m)` exactly the same as DFS.

### Implementation

The implementation of a BFS algorithm is not as simple as with the DFS but in this section, we'll see the most typical method that is based on a queue of nodes. The algorithm works as follows: First, we define a queue of nodes, I normally like to name it "BFS", and we push the origin (starting node). Here is the interesting part: while the queue is not empty, we are going to save the front of the queue and remove it no matter what, then we check all of the adjacent nodes to that saved node and push them to the queue but **only if they are not visited**, this process is going to repeat until the queue is empty.

If you don't know what a queue is, check out this section on my post about stacks and queues: https://blog.garybricks.com/stacks-and-queues-a-beginners-overview#heading-what-is-a-queue just understand the main idea and come back here since we are going to use c++ handy implementation.

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

int main() {
  int n, k;
  cin >> n >> k;
  vector<vector<int>> GRAPH(n + 1);
  vector<int> distance(n + 1, -1);
  for (int i = 0; i < k; i++) {
    int a, b;
    cin >> a >> b;
    GRAPH[a].push_back(b);
    GRAPH[b].push_back(a);
  }
  queue<int> BFS;
  BFS.push(1);
  distance[1] = 0;
  while (!BFS.empty()) {
    int current = BFS.front();
    BFS.pop();
    cout << "currently on:" << current << endl;
    for (auto node : GRAPH[current])
      if (distance[node] == -1) {
        distance[node] = distance[current] + 1;
        BFS.push(node);
      }
  }

  for (int i = 1; i <= n; i++)
    cout << "Node:" << i << " is " << distance[i]
         << " nodes away from node 1\n";
  return 0;
}
```

In the code cell above you can see my implementation in c++ using an adjacency list to represent the graph, notice how instead of using a vector of bools to see if a node has been visited we use a vector of ints to save the "distance" to node 1. For this case, I decided to initialize that distance vector with -1, "-1" is going to represent a node that has not been visited. Just like DFS, try to change the origin to see what the output is.

## DFS, BFS - Practice

In this section, we'll see some competitive programming problems I've faced and how they were solved using a DFS or BFS algorithm, at the same time we dive a little deeper into the topic and learn new things, read the problems and try to solve them by yourself, don't worry, the solutions are at the end of this section.

### 1 - Escape The Maze

Given a Matrix of characters representing a maze, where "\*" represents a wall, "E" represents the entry to the maze, and "X" the exit, print whether is possible or not to reach "X" starting from "E" through the empty spaces. Examples:

![MazeExamples.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1666474169273/7zxWAVg2G.png align="left")

### 2 - Water Puddles

Given a Matrix of characters of size **n \* m** in which **"w"** represents water and **"L"** represents land, output how many puddles of water are on the map and the size of the biggest one.

#### IMPORTANT NOTES:

A puddle is considered valid if it's **completely** surrounded by land, this means that any body of water touching the edges of the map does not count as a puddle.

Any body of water is considered connected to another if it's orthogonally or diagonally adjacent to it. See the examples below:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670021555040/0c88f3e4-545e-4c2a-b7e1-85f9d73ff515.png align="left")

### 3 - Oil Spill Simulation

Given a Matrix of characters of size n\*m in which "." represents water, "#" land, "\*" contaminated water, and "$" represents an oil plant that has a spill that every day spreads to an orthogonally adjacent square of water. Output what the Matrix will look like after k days. Example:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670199909093/aCjx5Lpom.png align="left")

### 4 - Safest Place

It's 2020 and covid is all over the place, as a responsible human you are trying to stay as furthest away from other people.

Given a Matrix of characters of size n\*m in which "#" represents a wall, "." an empty space, and "G" a person. find the empty square in which you can be the furthest from everyone. Example:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670529308820/EN7RfGVG1.png align="center")

Output the coordinates of the safest place, for the examples above this would be the answer:

```cpp
3 2
4 4
```

### 5 - King Escape

You are given a chess board of size n\*n, the coordinates of an enemy queen, the coordinates of your king, and an exit coordinate, your job is to output whether or not the king can reach the exit coordinate without getting in check and following the king movement rules. If it's possible, output the coordinates the king took to reach the exit, and if it's not possible, output -1;

IMPORTANT:

*   For this problem, the enemy queen will never move.
    
*   If it's possible to reach the exit coordinate you have to output the **shortest** path the king took, if there are several answers output any of them.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670107659663/-eAXMxLCM.png align="left")

### 1 - Escape The Maze - Solution

This is a very classical problem, however, the tricky part of this problem was to figure out how to represent the graph in order to apply the DFS algorithm.

```cpp
#include <iostream>
#include <vector>

using namespace std;

struct node {
  int i, j;
};

int n, m;
vector<string> MAZE;
vector<vector<bool>> visited;
node E, X;

void getInput() {
  string row;
  cin >> n >> m;
  getline(cin, row);
  for (int i = 0; i < n; i++) {
    getline(cin, row);
    MAZE.push_back(row);
  }
}

void findStartEnd() {
  for (int i = 0; i < n; i++)
    for (int j = 0; j < m; j++) {
      if (MAZE[i][j] == 'e') E = {i, j};
      if (MAZE[i][j] == 'x') X = {i, j};
    }
}

bool valid(int i, int j) {
  if (i >= 0 && j >= 0 && i < n && j < m && MAZE[i][j] != '*' && !visited[i][j])
    return true;
  return false;
}

void DFS(node c) {
  visited[c.i][c.j] = true;
  if (valid(c.i + 1, c.j)) DFS({c.i + 1, c.j});
  if (valid(c.i - 1, c.j)) DFS({c.i - 1, c.j});
  if (valid(c.i, c.j + 1)) DFS({c.i, c.j + 1});
  if (valid(c.i, c.j - 1)) DFS({c.i, c.j - 1});
}

int main() {
  getInput();
  findStartEnd();
  visited.resize(n, vector<bool>(m, 0));
  DFS(E);

  if (visited[X.i][X.j])
    cout << "There is a solution!";
  else
    cout << "IT'S IMPOSSIBLE TO ESCAPE";
  return 0;
}
```

This is the solution I came up with, it's a bit longer than what we are used to, but don't worry, I carefully separated every part in order to make it as readable as possible. Notice how when working with this type of problem is very comfortable to have your graph and visited matrix global. You might be wondering where our Graph is, we'll get to that in a second, first, let's get the input using our `getInput()` function. You might already have noticed the problem does not give you a graph as we have seen above, this is where you must think and realize that you can represent the nodes as the coordinates in the `MAZE` matrix, that's why I defined a node structure that simply saves an **x** and **y** coordinates. Then, we call our `findStartEnd()` function, this simply iterates through the `MAZE` and finds the starting and ending nodes. Now we initialize our visited matrix, and finally, we send our DFS starting from the start node. The DFS works as follows: first, we mark the current node as visited as we normally do, here's the interesting part: notice how we don't have our adjacency matrix, that is because it's not necessary, we literally check the adjacent positions in the Matrix! to do that I defined a `valid()` function that simply checks if it's a valid node for the DFS to go, that function takes care of the walls, if it's visited, and for out-of-bounds cases, this is a perfect example of an implicit graph.

### 2 - Water Puddles - Solution

The tricky part of this problem was to figure out if a puddle is valid, and its size. Below you can find the code with the explanation.

```cpp
#include <iostream>
#include <vector>
using namespace std;

int n, m, numPuddles = 0, BiggestPuddle = 0;
vector<vector<char>> MAP;
vector<vector<bool>> visited;
vector<int> X = {1, -1, 0, 0, 1, -1, 1, -1};
vector<int> Y = {0, 0, 1, -1, 1, -1, -1, 1};

void init() {
  cin >> n >> m;
  MAP.resize(n, vector<char>(m));
  visited.resize(n, vector<bool>(m));
  for (auto &row : MAP)
    for (auto &e : row) cin >> e;
}

bool valid(int i, int j) {
  if (i >= 0 && j >= 0 && i < n && j < m && !visited[i][j] && MAP[i][j] == 'W')
    return true;
  return false;
}

void DFS(int i, int j, int &size, bool &puddle) {
  visited[i][j] = true;
  size++;
  if (i == 0 || j == 0 || i == n - 1 || j == m - 1) puddle = false;

  for (int d = 0; d < 8; d++) {
    if (valid(i + X[d], j + Y[d])) DFS(i + X[d], j + Y[d], size, puddle);
  }
}

int main() {
  init();
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++)
      if (MAP[i][j] == 'W' && !visited[i][j]) {
        int size = 0;
        bool isPuddle = true;
        DFS(i, j, size, isPuddle);
        if (isPuddle) {
          BiggestPuddle = max(BiggestPuddle, size);
          numPuddles++;
        }
      }
  }

  cout << "There are: " << numPuddles
       << " puddles in the map, the largest one has a size of: "
       << BiggestPuddle;
  return 0;
}
```

To solve this problem, we iterate over the map of chars and if we find water we are going to assume it's a valid puddle and send the `dfs` on that specific coordinate, notice how we have two more parameters: `size` and `isPuddle` which are always passed by reference: `&`, this is important since we want to be able to modify the variables. `DFS` is not very different from the others, we mark the current position as visited and send the `DFS` to the eight possible adjacent coordinates, the only difference is that we always increment the `size` variable and if we reach an edge of the Map, we are going to say that the puddle is not valid. Once the `DFS` is done, we check if it's a valid puddle, if true, we increment the number of puddles found, and we check if it's bigger than the biggest puddle.

### 3 - Oil Spill Simulation - Solution

Just by looking at the example, you can tell that a BFS algorithm behaves exactly the same, the tricky part was how to stop the BFS at the **k** day. Below you can find my code with the explanation.

```cpp
#include <iostream>
#include <queue>
#include <vector>
using namespace std;

struct node { int i, j, level; };

int N, M, days;
vector<vector<char>> MAP;
int X[4] = {0,1,0,-1};
int Y[4] = {1,0,-1,0};
node source;

void get_input() {
  cin >> N >> M >> days;
  MAP.resize(N, vector<char>(M));
  for (int i = 0; i < N; i++) {
    for (int j = 0; j < M; j++) {
      cin >> MAP[i][j];
      if (MAP[i][j] == '$') source = {i, j, 0};
    }
  }
}

void print() {
  for (auto e : MAP) {
    for (auto c : e) cout << c;
    cout << "\n";
  }
}

bool valid(int i, int j){ return i >= 0 && j >= 0 && i < N && j < M && MAP[i][j] == '.';}

int main() {
  get_input();
  queue<node> BFS;
  BFS.push(source);
  while (!BFS.empty()) {
    node e = BFS.front();
    BFS.pop();
    if (e.level >= days) break;
    for(int i=0; i<4; i++){
		if(valid(e.i + X[i], e.j + Y[i])){
			MAP[e.i + X[i]][e.j + Y[i]] = '*';
			BFS.push({e.i+X[i], e.j+Y[i], e.level+1});
		}
	}
  }
  print();
  return 0;
}
```

Just like the previous problems, we represented a node as the coordinates on the matrix, and notice how this node has an extra **level** variable, this is going to help us know how far we are from the origin which is going to help us stop the BFS.

The algorithm works as follows:

1.  while the BFS is not empty get the current node and remove it
    
2.  check if the node has a distance greater or equal to k. if so, end the algorithm.
    
3.  for each valid adjacent node, modify that node to become contaminated and add it to the BFS with a level increment.
    

Once the BFS finishes, print the final Map. This problem cannot be solved with a DFS due to the land that can ruin the simulation and give an incorrect result.

### 4 - Safest Place - Solution

One of the first ideas most people have is to send a BFS from every single empty space and get the distance to the **closest** person and by doing that, find the best square, however, this idea is extremely inefficient. Another idea can be to send a BFS from every single person and get the distance to every single empty square and then fuse them together on a final matrix that contains all of the minimum distances, and lastly just search for the biggest value.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670540476464/CNS0avWP-.png align="center")

This is the correct idea, however, creating a distance matrix for each person can bring a lot of implementation and memory problems, the best and easiest solution involves using just a single BFS and distance matrix, it turns out that is totally possible and easy to send a BFS algorithm from several origins. Below you can see my solution.

```cpp
#include <iostream>
#include <queue>
#include <vector>
using namespace std;

struct node {int i, j;};

int N, M;
vector<vector<char>> MAP;
vector<vector<int>> V; // Distance Matrix
int X[4] = {0,1,0,-1};
int Y[4] = {1,0,-1,0};
vector<node> people;

void get_input() { // get Map, initialize the visited matrix, find the people
  cin >> N >> M;
  MAP.resize(N, vector<char>(M));
  V.resize(N, vector<int>(M, -1)); // -1 represents not visited
  for (int i = 0; i < N; i++) {
    for (int j = 0; j < M; j++) {
      cin >> MAP[i][j];
      if (MAP[i][j] == 'G') people.push_back({i, j});
    }
  }
}
// checks if the node is inside bounds, is an empty square, and is not visited
bool valid(int i, int j){ return i >= 0 && j >= 0 && i < N && j < M && MAP[i][j] == '.' && V[i][j]==-1;}

int main() {
  get_input();
// instead of adding a single source, we add all people.
  queue<node> BFS;
  for(auto e:people){BFS.push(e); V[e.i][e.j] = 0;}
  while (!BFS.empty()) {
    node e = BFS.front();
    BFS.pop();
    for(int i=0; i<4; i++){
		if(valid(e.i + X[i], e.j + Y[i])){
			V[e.i + X[i]][e.j + Y[i]] = V[e.i][e.j] + 1;
			BFS.push({e.i+X[i], e.j+Y[i]});
		}
	}
  }
  node result; // final search for the maximum value
  int maxi = -1;
  for(int i=0; i<N; i++){
    for(int j=0; j<M; j++)if(V[i][j] > maxi){
      maxi = V[i][j];
      result = {i, j};
    }
  }
  cout << result.i << " " << result.j;
  return 0;
}
```

This is a very standard BFS the big difference is how we define our visited matrix, for a DFS algorithm we normally use booleans but for a BFS we can actually save ints that represent the distance, and by doing that we can know the minimum distance from the origin to ANY other square which is going to be really helpful. And lastly, instead of sending the BFS from a single origin, we initialize the BFS with all of the nodes representing people, after that the algorithm remains the same.

Once the BFS is done, we are going to have our perfect visited matrix with all of the correct distances and we just need to find the maximum value.

### 5 - King Escape - Solution

This problem was very similar to the escape maze problem, however, the problem was that if there was a solution, you had to output the shortest route the king took, because of this, a **BFS** algorithm was the right choice. Below you can see my implementation with the explanation.

```cpp
#include <algorithm>
#include <iostream>
#include <queue>
#include <vector>
using namespace std;

struct node {
  int x, y;
};
vector<int> X = {1, -1, 0, 0, 1, -1, 1, -1};  // directions
vector<int> Y = {0, 0, 1, -1, 1, -1, -1, 1};  // directions
int n, qx, qy, kx, ky, ex, ey;
vector<vector<bool>> M;     // 0 = empty, 1 = check
vector<vector<int>> V;      // distance MAP
vector<vector<node>> BACK;  // Helper for recreating path
vector<node> path; // final path

void initBoard() {
  M.resize(n, vector<bool>(n, 0));
  V.resize(n, vector<int>(n, -1));
  BACK.resize(n, vector<node>(n, {-1, -1}));
  for (int i = 0; i < n; i++) {
    M[qx][i] = 1;
    M[i][qy] = 1;
  }
  int x = qx, y = qy;
  while (x >= 0 && y >= 0) {
    M[x][y] = 1;
    x--, y--;
  }
  x = qx, y = qy;
  while (x >= 0 && y < n) {
    M[x][y] = 1;
    x--, y++;
  }
  x = qx, y = qy;
  while (x < n && y >= 0) {
    M[x][y] = 1;
    x++, y--;
  }
  x = qx, y = qy;
  while (x < n && y < n) {
    M[x][y] = 1;
    x++, y++;
  }
}
// checks if it's not visited, not in check and inside the board.
bool valid(int x, int y) { 
  return x >= 0 && y >= 0 && x < n && y < n && !M[x][y] && V[x][y] == -1;
}

int main() {
  cin >> n >> qx >> qy >> kx >> ky >> ex >> ey;
  qx--, qy--, kx--, ky--, ex--, ey--;
  initBoard();
  queue<node> BFS;
  BFS.push({kx, ky});
  V[kx][ky] = 0;
  while (BFS.size()) {
    node current = BFS.front();
    BFS.pop();
    for (int i = 0; i < 8; i++) {
      if (valid(current.x + (X[i]), current.y + (Y[i]))) {
        V[current.x + (X[i])][current.y + (Y[i])] = V[current.x][current.y] + 1;
        BACK[current.x + (X[i])][current.y + (Y[i])] = current;
        BFS.push({current.x + (X[i]), current.y + (Y[i])});
      }
    }
  }
  if (V[ex][ey] == -1) { // checking if the escape square was not visited
    cout << -1;
    return 0;
  }
  node current = {ex, ey};
  while (!(current.x == -1 && current.y == -1)) {
    path.push_back(current);
    current = BACK[current.x][current.y];
  }
  reverse(path.begin(), path.end());
  cout << "-------------\n";
  for (int i = 1; i < path.size(); i++)
    cout << path[i].x + 1 << " " << path[i].y + 1 << " => ";
  return 0;
}
```

Just like every problem until now, we need to represent our graph, in this case, we can create a Matrix as the chessboard, and the values of the matrix can be either 0 or 1 where 1 is going to represent a square under check. We also create our distance matrix which is going to be helpful.

In order to "reconstruct" the path we are going to need an additional BACK matrix this is a brilliant way to know the square a square comes from. And lastly, we have our directions array that is going to help later on in pointing to the adjacent squares.

First, we initialize our Graph "M" with the `initBoard()` function which means marking every queen attacking square as "check".

Then we send our BFS on the king square and for each valid adjacent square we update the distance on the Visited Matrix "V", we also update our BACK matrix and send the BFS.

```cpp
if (valid(current.x + (X[i]), current.y + (Y[i]))) {
// the adjacent node is going to have a distance of the current node +1
V[current.x + (X[i])][current.y + (Y[i])] = V[current.x][current.y] + 1;
// the adjacent node is going to come from the current node
BACK[current.x + (X[i])][current.y + (Y[i])] = current;
BFS.push({current.x + (X[i]), current.y + (Y[i])});}
```

Once the BFS finishes. we check if the escape square was not visited, if this is the case, we output -1 else we can reconstruct the path by starting from the escape square and going back until it's no longer possible.

```cpp
  node current = {ex, ey};
  while (!(current.x == -1 && current.y == -1)) {
    path.push_back(current);
    current = BACK[current.x][current.y];
  }
  reverse(path.begin(), path.end());
```

Notice how we created a final path vector of nodes, and we push\_back the current position, this is going to give us the final route backward, that's why we have to use the reverse() method.

## **Conclusion - Farewell**

You've reached the end of this lesson on BFS and DFS, remember that this is a skill that takes a lifetime to master so don't feel frustrated if you don't get it right away because this isn't easy, but I hope some of the guidelines we saw today were helpful and the basic foundations on this topic were well understood, remember, there is still a lot to learn and we definitively didn't cover everything on Graphs, but I hope this was a good beginner overview and that you managed to grasp the basic ideas.

Let me know in the comments what you thought about this post and let me know what you will like to see next. Stay tuned!