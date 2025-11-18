
# EX 5B Topological Sort - Khan's Algorithm
## DATE: 27-10-2025
## AIM:
To write a Java program to for given constraints.
Problem Description:
A software development team is preparing for a product release. The release consists of multiple tasks, each dependent on other tasks being completed first. You are to determine a valid order in which all tasks can be completed. If it's not possible due to cyclic dependencies, output that the release cannot be scheduled.

Each task is labeled from 0 to n-1. The dependencies are provided in the form of pairs [a, b] which means task a depends on task b.

Implement a program to find a valid task execution order using topological sort.

Input Format:

An integer n — number of tasks.

An integer m — number of dependencies.

m lines follow with two integers a and b — representing a depends on b.

Output Format:

If a valid order exists, print the task numbers in a possible execution order (space-separated).

If not, print "Release cannot be scheduled".

<img width="341" height="363" alt="image" src="https://github.com/user-attachments/assets/f0355541-4f66-49da-bcd3-171a799a7c1f" />

## Algorithm:
1. Build an adjacency list and compute in-degree for all tasks.

2. Insert all tasks with in-degree = 0 into a queue.

3. Repeatedly remove a task from the queue, append it to the order.

4. For each of its neighbours, reduce in-degree and push those reaching zero into the queue.

5. If all tasks are processed, return the order; otherwise, cycle exists → scheduling impossible.   

## Program:
```
Developed by: SAI VISHAL D
Register Number: 212223230180

import java.util.*;

public class prog{

    public static List<Integer> findTaskOrder(int n, int[][] dependencies) {
        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i < n; i++) adj.add(new ArrayList<>());
        int[] indeg = new int[n];
        for (int[] d : dependencies) {
            int a = d[0], b = d[1];
            adj.get(b).add(a);
            indeg[a]++;
        }
        Queue<Integer> q = new ArrayDeque<>();
        for (int i = 0; i < n; i++) if (indeg[i] == 0) q.add(i);
        List<Integer> order = new ArrayList<>();
        while (!q.isEmpty()) {
            int u = q.poll();
            order.add(u);
            for (int v : adj.get(u)) {
                indeg[v]--;
                if (indeg[v] == 0) q.add(v);
            }
        }
        return order.size() == n ? order : null;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int m = sc.nextInt();
        int[][] dependencies = new int[m][2];
        for (int i = 0; i < m; i++) {
            dependencies[i][0] = sc.nextInt();
            dependencies[i][1] = sc.nextInt();
        }
        List<Integer> result = findTaskOrder(n, dependencies);
        if (result == null) System.out.println("Release cannot be scheduled");
        else {
            for (int task : result) System.out.print(task + " ");
            System.out.println();
        }
        sc.close();
    }
}

```

## Output:

<img width="670" height="510" alt="image" src="https://github.com/user-attachments/assets/7bd4ac0c-abf8-4647-9300-b4b34f3e0fc1" />



## Result:
The program successfully implemented and the expected output is verified.
