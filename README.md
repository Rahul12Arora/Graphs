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
