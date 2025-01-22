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
**6. Buy and sell Stock**
You are given an array prices where prices[i] is the price of a given stock on the ith day.
You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.
Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

Example 1:
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.


**My approach**
```
public class StockSell {

	public static void main(String[] args) {
		//get array 
		//buy the stock
		//traverse the array after stock buy date 
		//if greater value found sell it else return zero no profit 
	    int[] prices = {7, 1, 5, 3, 6, 4};
	    
	    int maxProfit =0;
	    
	    for(int i=0; i< prices.length;i++) {
	    	for(int j = i+1;j < prices.length; j++) {
	    		int profit = prices[j] - prices[i];
	    		
	    		if(profit>maxProfit) {
	    			maxProfit = profit;
	    		}
	    	}
	    }

	    System.out.println("Maximum Profit: " + maxProfit);
	}

}
```
Now optimising it for only one for loop 
Time complexity -O(n)
Space complexity - O(1)
```
public class StockSell {

	public static void main(String[] args) {
	    int[] prices = {7, 1, 5, 3, 6, 4};

            //varible to store the maximium profit 
	    int maxProfit =0;
            //varible to store minimum price encountered so far 
	    int minPrice = Integer.MAX_VALUE;
	    //loop through array to calculate maximum profit 
	    for(int i=0; i< prices.length;i++) {
            //update minPrice if the current price is lower than the previous minPrice
	    	if(prices[i] < minPrice) {
	    		minPrice = prices[i];
	    	}
             //calculate the profit if we sold at current price	
	    	int profit = prices[i] - minPrice;
	    	//update maxProfit if the current profit is higher than previous maxProfit
	    	if(profit>maxProfit) {
	    		maxProfit = profit;	
	    	}
	    }
	    System.out.println("Maximum Profit: " + maxProfit);
	}
}
```
**7. Buy and sell Stock II**

You are given an integer array prices where prices[i] is the price of a given stock on the ith day.

On each day, you may decide to buy and/or sell the stock. You can only hold at most one share of the stock at any time. However, you can buy it then immediately sell it on the same day.

Find and return the maximum profit you can achieve.

Example 1:

Input: prices = [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
Total profit is 4 + 3 = 7.

**My Approach**
```
public class StockSell {

	public static void main(String[] args) {
	    int[] prices = {7, 1, 5, 3, 6, 4};
	    
	    int maxProfit =0;
	        for(int i=1;i< prices.length;i++) {
	        	if(prices[i] > prices[i-1]) {
	        		maxProfit += prices[i] - prices[i-1];
	        	}
	    }
	    System.out.println("Maximum Profit: " + maxProfit);
	}
}
```

**8. Majority Element**
Given an array nums of size n, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

Example 1:
Input: nums = [3,2,3]
Output: 3
Example 2:

Input: nums = [2,2,1,1,1,2,2]
Output: 2
 
**My Approach**
```
public class MajorityElement {

	public int majorityElement(int[] nums) {
		int n=nums.length;
		for(int i=0;i<n;i++) {
			int count = 0;
			for(int j =0;j<n;j++) {
				if(nums[j]==nums[i]) {
					count++;
				}
			}
			if(count > n/2) {
				return nums[i];
			}
		  }		
			return -1;
		}
	public static void main(String[] args) {
		
		MajorityElement mj = new MajorityElement();
		
		int[] nums1 = {3,2,3};
		System.out.println(mj.majorityElement(nums1));

	}

}
```

Now we will reduce the space complexity and time complexity to linear time ;
we will use BOYER MOORE Voting algorithm for this .

```
public class MajorityElement {

	public int majorityElement(int[] nums) {
		    int candidate = nums[0];
		    int count = 1;
		    
		    for(int i=1;i<nums.length;i++) {
		    	if(count == 0) {
		    		candidate = nums[i];
		    		count = 1;
		    	}else if(nums[i] == candidate) {
		    		count++;
		    	}else {
		    		count--;
		    	}
		    }
			return candidate;
}
	public static void main(String[] args) {
		
		MajorityElement mj = new MajorityElement();
		
		int[] nums1 = {2,2,1,1,1,2,2};
		System.out.println(mj.majorityElement(nums1));

	}
}
```

**9. RemoveDuplicate from array**
Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in nums.

Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. The remaining elements of nums are not important as well as the size of nums.
Return k.
Custom Judge:

The judge will test your solution with the following code:

int[] nums = [...]; // Input array
int[] expectedNums = [...]; // The expected answer with correct length

int k = removeDuplicates(nums); // Calls your implementation

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
    assert nums[i] == expectedNums[i];
}
If all assertions pass, then your solution will be accepted.

 **My Approach**
```
public class RemoveDupArray {
    public int removeDuplicates(int[] nums) {
    	if(nums.length==0) {
    		return 0;
    	}
    	int k = 1;
    	
    	for(int i=1;i<nums.length;i++) {
    		if(nums[i]!= nums[i -1]) {
    			nums[k] = nums[i];
    			k++;
    		}
    	}
    	return k;
    }
	
	public static void main(String[] args) {	
         RemoveDupArray r = new RemoveDupArray();    
         int[] nums = {1, 1, 2, 2, 3, 4, 4, 5};     
         int k = r.removeDuplicates(nums);
         System.out.println("Number of unique elements: " + k);
         System.out.print("Array after removing duplicates: [");
         for (int i = 0; i < k; i++) {
             System.out.print(nums[i] + (i < k - 1 ? ", " : ""));
         }
         System.out.println("]");
	}
}
```

**10. Square of a array**

Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

Example 1:
Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].

**My Approach**
```
public class SquareAndSortArray {

	public int[] sortedSquares(int[] nums) {
		int n = nums.length;
		for(int i=0;i<n;i++) {
			nums[i]=nums[i]*nums[i];
		}
		
		for(int i=0;i<n-1;i++) {
			for(int j = 0;j<n-i-1;j++) {
				if(nums[j]>nums[j+1]) {
					int temp = nums[j];
					nums[j] = nums[j+1];
					nums[j+1] = temp;
				}
			}
		}
		return nums;
	}
	public static void main(String[] args) {
		SquareAndSortArray sol = new SquareAndSortArray();
		int[] nums1 = {-4,-1,0,3,10};
		int[] result = sol.sortedSquares(nums1);
		for(int num: result) {
			System.out.print(num+" ");
		}
	}

}
```
