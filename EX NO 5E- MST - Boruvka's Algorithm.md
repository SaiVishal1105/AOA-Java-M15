
# EX 5E Minimum Spanning Tree -Boruvka's Algorithm
## DATE: 06-11-2025
## AIM:
To write a Java program to for given constraints.
Boruvka's Algorithm - Minimum Spanning Tree

Find the MST using Boruvka's Algorithm for a weighted undirected graph.

<img width="292" height="235" alt="image" src="https://github.com/user-attachments/assets/06246b27-37a9-40a8-bd7a-37a1d5187cd1" />

## Algorithm
1. Initialize each vertex as its own component using the Disjoint Set (Union–Find) structure.

2. For every component, find the cheapest outgoing edge connecting it to any other component.

3. Add all such cheapest edges to the MST and merge their components (Union operation).

4. Repeat the process of finding cheapest edges for the newly formed components.

5. Stop when only one component remains, and the collected edges form the Minimum Spanning Tree.

## Program:
```
Developed by: SAI VISHAL D
Register Number: 212223230180  

import java.util.*;

public class BoruvkaMST {
    static int[] parent;
    static int find(int i) {
        if (parent[i] != i) parent[i] = find(parent[i]);
        return parent[i];
    }
    static void union(int x, int y) {
        parent[find(x)] = find(y);
    }
    static int boruvkaMST(int V, List<Edge> edges, List<Edge> mstEdges) {
        parent = new int[V];
        for (int i = 0; i < V; i++) parent[i] = i;
        int components = V;
        int totalWeight = 0;
        int[] cheapest = new int[V];
        Arrays.fill(cheapest, -1);
        while (components > 1) {
            Arrays.fill(cheapest, -1);
            for (int i = 0; i < edges.size(); i++) {
                Edge e = edges.get(i);
                int setU = find(e.src);
                int setV = find(e.dest);
                if (setU == setV) continue;
                if (cheapest[setU] == -1 || edges.get(cheapest[setU]).weight > e.weight) cheapest[setU] = i;
                if (cheapest[setV] == -1 || edges.get(cheapest[setV]).weight > e.weight) cheapest[setV] = i;
            }
            boolean anyMerged = false;
            for (int i = 0; i < V; i++) {
                int idx = cheapest[i];
                if (idx == -1) continue;
                Edge e = edges.get(idx);
                int setU = find(e.src);
                int setV = find(e.dest);
                if (setU == setV) continue;
                union(setU, setV);
                totalWeight += e.weight;
                mstEdges.add(e);
                components--;
                anyMerged = true;
            }
            if (!anyMerged) break;
        }
        return totalWeight;
    }
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int V = sc.nextInt();
        int E = sc.nextInt();
        List<Edge> edges = new ArrayList<>();
        for (int i = 0; i < E; i++) edges.add(new Edge(sc.nextInt(), sc.nextInt(), sc.nextInt()));
        List<Edge> mstEdges = new ArrayList<>();
        int totalWeight = boruvkaMST(V, edges, mstEdges);
        for (Edge e : mstEdges) System.out.println("Edge: " + e.src + "-" + e.dest + " Weight: " + e.weight);
        System.out.println("Total Weight of MST: " + totalWeight);
        sc.close();
    }
}

class Edge {
    int src, dest, weight;
    Edge(int s, int d, int w) { src = s; dest = d; weight = w; }
}

```

## Output:
<img width="612" height="463" alt="image" src="https://github.com/user-attachments/assets/a33942d9-2a69-4544-9ef4-2b85b6d66166" />




## Result:
The program successfully implemented and the expected output is verified.
