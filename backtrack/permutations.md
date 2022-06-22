# Permutations

### Problem Statement

Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

### Key Takeaway

Permutation means that all elements are included and the order counts.

### Solution

```java
class Solution {
    List<List<Integer>> res= new ArrayList<>();
    LinkedList<Integer> path = new LinkedList<>();
    boolean[] used;

    public List<List<Integer>> permute(int[] nums){
        // Rule out the corner case first
        if(nums.length == 0){
            res.add(path);
            return res;
        }

        used = new boolean[nums.length];
        backtrack(nums);

        return res;
    }

    private void backtrack(int[] nums) {
        if(path.size() == nums.length){
            res.add(new ArrayList<>(path));
            return;
        }
        for(int i=0; i<nums.length; i++){
            if(!used[i]){
                path.add(nums[i]);
                used[i] = true;
                backtrack(nums);
                used[i] = false;
                path.removeLast();
            }
        }

    }
}
```

# Permutations II

### Problem Statement

Given a collection of numbers, nums, that might contain duplicates, return all possible unique permutations in any order.

### Key Takeaway

There may exist duplicate in nums. In order to rule out the duplicate, same strategy used in subsets can be applied.

### Solution

```java
class Solution {
    List<List<Integer>> res = new ArrayList<>();
    LinkedList<Integer> path = new LinkedList<>();
    boolean[] used;
    public List<List<Integer>> permuteUnique(int[] nums){
        if(nums.length == 0){
            res.add(path);
            return res;
        }

        Arrays.sort(nums);
        used = new boolean[nums.length];

        backtrack(nums);

        return res;
    }

    private void backtrack(int[] nums){
        if(path.size() == nums.length){
            res.add(new ArrayList<>(path));
            return;
        }

        for(int i=0; i<nums.length; i++){
            if(!used[i]){
                if(i>0 && nums[i] == nums[i-1] && !used[i-1]){
                    continue;
                }
                used[i] = true;
                path.add(nums[i]);
                backtrack(nums);
                path.removeLast();
                used[i] = false;
            }
        }
    }
}
```
