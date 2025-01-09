# BFS-3

## Problem1 Remove Invalid Parentheses(https://leetcode.com/problems/remove-invalid-parentheses/)
## Time Complexity:O(2^N) Space Complexity:O(N)
class Solution {
    public List<String> removeInvalidParentheses(String s) {
        List<String> result=new ArrayList<>();
        if(s==null || s.length()==0) return result;


        Queue<String> q=new LinkedList<>();
        q.add(s);


        HashSet<String> set=new HashSet<>();
        set.add(s);

        boolean flag=false;

        while(!q.isEmpty() && !flag)
        {
            int size=q.size();

            for(int i=0;i<size;i++)
            {
                String curr=q.poll();
                if(isValid(curr)){
                   result.add(curr);
                   flag=true;
                }
                
                else{
                    if(!flag)
                    {
                    for(int k=0;k<curr.length();k++)
                    {   if(Character.isAlphabetic(curr.charAt(k))) continue;
                        String baby=curr.substring(0,k)+curr.substring(k+1);
                        if(!set.contains(baby))
                        {
                            set.add(baby);
                            q.add(baby);
                        }
                    }
                    }
                }
            }
        }
        return result;
    }


    private boolean isValid(String s)
    {
        int count=0;

        for(char c:s.toCharArray()){
            if(Character.isAlphabetic(c)) continue;
            if(c=='(')
            count++;
            else
            count--;

            if(count<0) return false;

        
        }
        return count==0;
    }
}

## Problem2 Clone graph (https://leetcode.com/problems/clone-graph/)
## Time Complexity:O(V+E) Space Complexity:O(V)

/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> neighbors;
    public Node() {
        val = 0;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val) {
        val = _val;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val, ArrayList<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
}
*/

class Solution {
    HashMap<Node,Node> map;

    public Node cloneGraph(Node node) {
        if(node==null) return null;
       this.map=new HashMap<>();
       Queue<Node> q=new LinkedList<>();
       q.add(node);


       while(!q.isEmpty()){
        Node curr=q.poll();
        Node copyCurr=clone(curr);
        for(Node ne:curr.neighbors){
            if(!map.containsKey(ne)){
                q.add(ne);

            }
            copyCurr.neighbors.add(clone(ne));
        }
       }
       return map.get(node);

    }


    private Node clone(Node node)
    { 
        if(node==null) return null;
        if(!map.containsKey(node)){
            map.put(node,new Node(node.val));
        }
        return map.get(node);
    }
}
