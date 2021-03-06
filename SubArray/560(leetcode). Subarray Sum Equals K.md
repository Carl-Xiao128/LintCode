### 解题思路 Solution-1 Subarray Sum Equals K
#### 使用hashMap解决
- - -
### 题解代码
```java
public class Solution {
    public int subarraySum(int[] nums, int k) {

        if(nums == null || nums.length == 0){
            return 0;
        }

        if(nums.length == 1){
            return nums[0] == k ? 1 : 0;
        }

        int count = 0, sum = 0;
        HashMap<Integer, Integer> map = new HashMap<>();

        map.put(0, 1);

        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];           
            if (map.get(sum - k) != null){
                count += map.get(sum - k);
            }

            if(map.get(sum) == null){
                map.put(sum, 0);
            }
            map.put(sum, map.get(sum) + 1);
        }
        return count;
    }
}
```

### 解题思路 Solution-2 Subarray Sum Equals K
#### 使用hashMap解决, 使用map.getOrDefault简化代码
- - -
### 题解代码
```java
public class Solution {
    public int subarraySum(int[] nums, int k) {

        if(nums == null || nums.length == 0){
            return 0;
        }

        if(nums.length == 1){
            return nums[0] == k ? 1 : 0;
        }

        int count = 0, sum = 0;
        HashMap<Integer, Integer> map = new HashMap<>();

        map.put(0, 1);

        for(int num : nums){
            sum += num;
            count += map.getOrDefault(sum - k, 0);
            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }

        return count;
    }
}
```
### 解题思路 Solution-3 Subarray Sum Equals K
#### 使用PrefixSum + hashMap解决
- - -
### 题解代码
```java
public class Solution {
    public int subarraySum(int[] nums, int k) {
        int count = 0;

        if(nums == null || nums.length == 0){
            return count;
        }

        int n = nums.length;
        int[] prefixSum = new int[n + 1];
        for(int i = 1; i <= n; i++){
            prefixSum[i] = prefixSum[i -1] + nums[i - 1];
        }

        HashMap<Integer, Integer> map = new HashMap<>();

        for(int i = 1; i <= n; i++){
            if(prefixSum[i] == k){
                count++;
            }

            if(map.containsKey(prefixSum[i] - k)){
                count += map.get(prefixSum[i] - k);
            }

            map.put(prefixSum[i], map.getOrDefault(prefixSum[i], 0) + 1);
        }
        return count;
    }
}
```
