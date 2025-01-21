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
**2. Check if a number is palindrome or not**
Given an integer x, return true if x is a 
palindrome, and false otherwise. 

Example 1:
Input: x = 121
Output: true
Explanation: 121 reads as 121 from left to right and from right to left.

**My approach**
```
public class Palindrome {

	public boolean isPalindrome(int x) {
		//edge case : negative and multiple of 10 are not palindrome
		if(x<0 || (x%10 == 0 && x!=0)) {
			return false;
		}
		int reversed = 0;
		
		//reverse the second half of the number
		while(x > reversed) {
			reversed = reversed*10 + x%10;
			x/=10;
		}
		//check original is equal to reversed or not , in case of odd length if middle digit doesnt match ignore
		return x == reversed ||  x == reversed /10;
	}
	public static void main(String[] args) {
		Palindrome p = new Palindrome();
		System.out.println("test case 1:" + p.isPalindrome(121));			
	}
}
```

Now  using jStrings this progam can be 
```
public class Palindrome {

	public boolean isPalindrome(int x) {
		//edge case : negative number and multiple of 10 can't be palindrome
		if(x<0 || (x% 10 == 0 && x!=0)) {
			return false ;
		}
		
		String original = Integer.toString(x);
		String reversed = new StringBuilder(original).reverse().toString();
		
		return original.equals(reversed);
	}
	public static void main(String[] args) {
		Palindrome p = new Palindrome();
		System.out.println("test case 1:" + p.isPalindrome(141));			
	}
}
```
**3. PlusOne**
You are given a large integer represented as an integer array digits, where each digits[i] is the ith digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading 0's.

Increment the large integer by one and return the resulting array of digits.

Example 1:

Input: digits = [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
Incrementing by one gives 123 + 1 = 124.
Thus, the result should be [1,2,4].


**My approach**
```
public class IncrementByOne {
	public int[] plusOne(int[] digits) {
		//get the length
		int n = digits.length;
		
		//last to first
		for(int i=n-1;i>=0;i--) {
			//if digit less than 9 increment and return
			if(digits[i] < 9) {
				digits[i] +=1;
				return digits;
			}
			//if digit is 9 set current to 0 and carry over
			digits[i] = 0;
		}
		
		int[] result = new int[n+1];
		result[0] = 1; //set leading digit to 1
		return result;  // rest will be zero
	}	
	
	public static void main(String[] args) {
		IncrementByOne sol = new IncrementByOne();	
		int[] digits1 = {1,2,9};
		System.out.println(Arrays.toString(sol.plusOne(digits1)));
	}

}
```

**4. Move Zeros**

Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.
Note that you must do this in-place without making a copy of the array.

Example 1:

Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]


**My Approach**
```
public class MoveZerosArray {
	private void moveZeroes(int[] nums) {
		int lastNonZero =0;  //get position to place non zero element
		
		//traverse through array
		for(int i=0;i<nums.length;i++) {
			if(nums[i]!=0) {
				nums[lastNonZero] = nums[i]; //if current not zero move to lastnonzero
				if(i!= lastNonZero) {    //increment non zero element
					nums[i] =0;
				}
				lastNonZero++;  //increment next non zero element
			}
		}	
	}
	
	public static void main(String[] args) {
		MoveZerosArray sol = new MoveZerosArray();
		
		int[] nums1 = {0,1,0,3,12};
		sol.moveZeroes(nums1);
		System.out.println(Arrays.toString(nums1));
	}
}
```
**5. Fibanacci Series**

The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. That is,
F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2), for n > 1.
Given n, calculate F(n). 

Example 1:
Input: n = 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.

**My approach**
```
public class Fibanacci {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
        
		System.out.println("Enter the value of n");
		int n = scanner.nextInt();
		
		if(n==0) {
			System.out.println("F("+ n +") = 0");
		}else if(n==1) {
			System.out.println("F("+ n + ") = 1");
		}else {
			int a=  0;
			int b=1;
			int c=0;
			
			for(int i=2;i<=n;i++) {
				c = a+b;  //this is the approach
				a=b;
				b=c;
			}
			System.out.println("F("+ n +")= "+ c);
		}
		scanner.close();
	}
}
```
Leet code accepted code :
```
public class Fibanacci {
    public int fib(int n) {
    	if(n == 0) return 0;
    	if(n ==1) return 1;
    	
    	int a=0,b=1;
    	
    	for(int i=2;i<=n;i++) {
    		int c = a + b;  //Fn = Fn-1 + Fn-2;
    		a = b;  //move the previous fibanacci number 
    		b = c;  //update the new fibanacci number
    	}
    	return b; //b holds the calue of F(n)
    }
	public static void main(String[] args) {
		Fibanacci f = new Fibanacci();
		System.out.println(f.fib(5));
	}
}
```
