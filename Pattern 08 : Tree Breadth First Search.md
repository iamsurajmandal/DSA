https://leetcode.com/problems/maximum-level-sum-of-a-binary-tree/description/

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
1. Loop through the Tree until Queue is empty
2. Acuumlate the current sum at each level
3. compare previous maximum sum
     - update maximum sum if current sum is greater
4. retun the maximum sum level 

# Complexity
- Time complexity: O(n) each node visited once
<!-- Add your time complexity here, e.g. $$O(n)$$ -->

- Space complexity: O(n) Queue holds up to all nodes at one level
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

# Code
```java []
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public int maxLevelSum(TreeNode root) {
        Queue<TreeNode> queueBinary = new LinkedList<>();
        queueBinary.offer(root);
        int k = 1, maxLevel = 1;
        int maxSum = Integer.MIN_VALUE;
        while (!queueBinary.isEmpty()) {
            int queueLevel = queueBinary.size();
            int sum = 0;
            for (int i = 0; i < queueLevel; i++) {
                TreeNode current = queueBinary.poll();
                if (current.left != null ) queueBinary.offer(current.left);
                if (current.right != null ) queueBinary.offer(current.right);
                sum += current.val;
            }
            
            if (sum > maxSum ) {
                maxSum = Math.max(maxSum, sum);
                maxLevel = k;
            }
            k++;
        }
        return maxLevel;
    }
}
```
