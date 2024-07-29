# Graphs
Graph Data Structure Revision

BFS And DFS Traversal
```
class Solution {
    public boolean validPath(int n, int[][] edges, int source, int destination) {

        //making space for a graph to iterate through every node
        ArrayList<ArrayList<Integer>> graph = new ArrayList<ArrayList<Integer>>();

        //creating graph
        for(int i=0;i<n;i++){
            // System.out.print(i);
            graph.add(new ArrayList<Integer>());
        }
        for(int[] arr: edges){
            graph.get(arr[0]).add(arr[1]);
            graph.get(arr[1]).add(arr[0]);
        }

        //making a boolean array to mark visited nodes, hashset can also be user here
        boolean[] visited = new boolean[n];

        //queue to iterate in bfs manner
        Queue<Integer> holder = new LinkedList<>();

        //initializing the start point in queue
        holder.add(source);
        // boolean[] ans = new boolean[n];


        // //iterate until all nodes have been exhausted
        // while(!holder.isEmpty()){
        //     //handling current node
        //     int curr = holder.poll();
        //     // System.out.println("curr is " + curr);
        //     // System.out.println("visited[curr] is " + visited[curr]);

        //     //if current is answer we return true & break the loop
        //     if(curr==destination) return true;

        //     //if the node is new and unexplored, we add the children in queue to be explored
        //     if(!visited[curr]){
        //         // System.out.println("adding new children");
        //         visited[curr] = true;
        //         // System.out.println("graph.get(curr) length is " + graph.get(curr).size());
        //         for(int child : graph.get(curr)){
        //             // System.out.println(child);
        //             holder.add(child);
        //         }
        //     }

        //     // System.out.println("holder.length is " + holder.size());
        // }

        // return false;
        return recfun(graph,holder,visited,destination,source, n);
    }

    public boolean recfun(ArrayList<ArrayList<Integer>> graph, Queue<Integer> holder, boolean[] visited, int d, int curr, int n){
        if(curr == d) return true;

        if(visited[curr]==false){
            visited[curr]=true;
            
            for(int child : graph.get(curr)){
                if(recfun(graph, holder, visited, d, child, n)){
                    return true;
                }
            }
        }

        return false;
    }

}
```

**PRIM'S ALGORITHM** 

This is used for MST, prim's algo follows greedy Approach(Selecting the local best), we'll use a min Heap based on cost for object {target,cost} & a visited set; we'll take out the min cost object out and add if it's not in visited and discard if it is, when adding in visited we'll also add extra entries into heap for new costs originating from the current target point as source.

```
class Solution {
    public int minCostConnectPoints(int[][] points) {
        int n = points.length;
        HashSet<Integer> visited = new HashSet<Integer>();
        HashSet<Integer> unVisited = new HashSet<Integer>();
        for(int i=0;i<n;i++){
            unVisited.add(i);
        }
        PriorityQueue<TargetCostObj> costQueue = new PriorityQueue<TargetCostObj>(Comparator.comparingInt(e -> e.cost));
        costQueue.add(new TargetCostObj(0,0)); //signifies that there is a point from 0th to 0th with 0 cost
        
        int ans = 0;

        while(visited.size()<n || !costQueue.isEmpty()){
            TargetCostObj curr = costQueue.poll();
            // System.out.println("curr target is "+curr.target);
            // if there's a condition to add a node to visited SET
            if(!visited.contains(curr.target)){
                // System.out.println("visited has elements count " + visited.size());
                visited.add(curr.target);
                unVisited.remove(curr.target);
                ans+= curr.cost;

                int source = curr.target;
                // Add all new Targets with costs Eg-> point
                for(int i : unVisited){
                    if(!visited.contains(i)){
                        TargetCostObj newProp = new TargetCostObj(i, manhattenCost(points[i],points[source]));
                        costQueue.add(newProp);
                    }
                }
            }
        }
        return ans;

    }
    public int manhattenCost(int[] point1, int[] point2){
        return Math.abs(point1[0]-point2[0]) + Math.abs(point1[1]-point2[1]);
    }

    class TargetCostObj{
        int target;
        int cost;

        public TargetCostObj(int target, int cost){
            this.target=target;
            this.cost=cost;
        }
    }
}
```
