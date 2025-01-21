 **1. Two Sum**

 Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.
Example 1:
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

My Approach 
---
 ```
//time complexity =  O(n2) because of two nexted loops  , Space complexity = O(1)
public class TwoSum {	
	public int[] twoSum(int[] nums, int target) {
		for(int i = 0; i< nums.length;i++) {
			for(int j = i+1;j<nums.length;j++) {
				if(nums[i]+nums[j] == target) {
					return new int[] {i,j};
				}
			}
		}
		throw new IllegalArgumentException("No solution found");
	}
	

	public static void main(String[] args) {
		TwoSum solution = new TwoSum();
		
		int[] nums = {2,7,11,15};
		int target = 13;
		
		int[] result = solution.twoSum(nums, target);
		System.out.println("Indieces:" + result[0] + ", " + result[1]);
	}
}
```

To reduce its complexity we can use HASHMAP or HashTable to store the numbers which we have already visited which will allow us to check if the complement of current 
number exists in constant time. It will reduce the time complexity from O(n2) to O(n).

```
public class TwoSum {	
	public int[] twoSum(int[] nums, int target) {
		    HashMap<Integer,  Integer> numMap = new HashMap<>();
		    for(int i = 0; i< nums.length; i++) {
		    	int complement = target - nums[i];
		    	
		    	if(numMap.containsKey(complement)) {
		    		return new int[] {numMap.get(complement),i};
		    	}
		    	numMap.put(nums[i], i);
		}
		throw new IllegalArgumentException("No solution found");
	}
	
	public static void main(String[] args) {
		TwoSum solution = new TwoSum();
		
		int[] nums = {2,7,11,15};
		int target = 9;
		
		int[] result = solution.twoSum(nums, target);
		System.out.println("Indieces:" + result[0] + ", " + result[1]);
	}
}
```
we can more optimise this soltion by using get() to avoid two lookups in containsKey();

```
public class TwoSum {	
	public int[] twoSum(int[] nums, int target) {
		    HashMap<Integer,  Integer> numMap = new HashMap<>();
		    for(int i = 0; i< nums.length; i++) {
		    	int complement = target - nums[i];
		    	
		    	Integer index = numMap.get(complement);
		    	
		    	if(index!= null) {
		    		return new int[] {index,i};
		    	}
		    	numMap.put(nums[i], i);
		}
		throw new IllegalArgumentException("No solution found");
	}
	
	public static void main(String[] args) {
		TwoSum solution = new TwoSum();
		
		int[] nums = {2,7,11,15};
		int target = 9;
		
		int[] result = solution.twoSum(nums, target);
		System.out.println("Indieces:" + result[0] + ", " + result[1]);
	}
}
```
