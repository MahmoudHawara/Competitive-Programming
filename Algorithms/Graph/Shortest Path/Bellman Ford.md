# Bellman Ford

Single source shortest path with negative weight edges

## Use Cases

- to get `Shortest path` when The Graph contains `Negative Edges`.

- if the graph contains a negative cycle, then, clearly, the shortest path to some vertices may not exist *(due to the fact that the weight of the shortest path must be equal to minus infinity)*; however, this algorithm can be modified to `signal the presence of a cycle of negative weight`, or even `deduce this cycle`.

- if there are `multiple Negative Cycles`, this algorithm can tell that there is `at least one` Negative Cycle and `find one of them`. However, ***it cannot determine how many Negative Cycles exist or find all of them***.

## to Use

```sh
# In Global

const int N = 1e5 + 5;     # N  = The Maximum number of Nodes in The Graph
const ll OO = 1e18;        # OO = Infinity

int n;                     # n is The number of nodes in The graph

# Edge representation
struct Edge
{
    int u, v, w;
};

# grah representation
vector<Edge>edges;   

ll dis[N];
# this array after execution of the algorithm will contain the answer to the problem where d[i] = the shortest path from the source to node i.

ll par[N];
# this array used to retrieve the path
```

# No Negative Cycles

This Section when there is no Negative Cycles or for unreachable Negative Cycles.

The algorithm consists of several phases. Each phase scans through all edges of the graph, and the algorithm tries to produce `relaxation` along each edge `(u, v)` having weight `w`. Relaxation along the edges is an attempt to improve the value `dis[v]` using value `d[u] + w`. In fact, it means that we are trying to improve the answer for this vertex using edge `(u, v)` and current response for vertex `u`.

```sh
void bellman_ford(int source)
{
    for (int i = 0; i <= n; i++)
    {
        dis[i] = OO;
    }
    dis[source] = 0;
    while(true)
    {
        bool enhance = false;
        for (Edge e : edges)
            if (dis[e.u] != OO && dis[e.u] + e.w < dis[e.v])
            {
                dis[e.v] = dis[e.u] + e.w;
                enhance  = true;
            }
        if (enhance == false)break;
    }
}
```

## Retrieving Path

```sh
void bellman_ford(int source)
{
    for (int i = 1; i <= n; i++)
    {
        dis[i] = OO;
        par[i] = -1
    }
    dis[source] = 0;
    while(true)
    {
        bool enhance = false;
        for (Edge e : edges)
            if (dis[e.u] != OO && dis[e.u] + e.w < dis[e.v])
            {
                dis[e.v] = dis[e.u] + e.w;
                par[e.v] = e.u;
                enhance  = true;
            }
        if (enhance == false)break;
    }
}

vector<ll> getPath(int node)
{
    vector<ll>path;
    for (int v = node; v != -1; v = par[v])
    {
        path.push_back(v);
    }
    reverse(path.begin(), path.end());
    return path;
}
```