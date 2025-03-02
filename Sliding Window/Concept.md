# Sliding Window

### References-
Youtube CodeStoryWithMIK: [Concepts and Problems](https://www.youtube.com/playlist?list=PLpIkg8OmuX-J2Ivo9YdY7bRDstPPTVGvN)


### Base Template:
```cadence
// Problem : https://leetcode.com/problems/contains-duplicate-ii/description/

bool containsNearbyDuplicate(vector<int>& nums, int k) {
    int n = nums.size();
    unordered_map<int, int> mp;

    // Two pointers to maintain start and end of window
    int i,j;
    i=j=0;

    while(j<n){
        // Take the element and expand the window
        mp[nums[j]]++;

        // Check if it is a Valid Window, If not decrease until valid and take answer
        if(abs(i-j)>k){
            mp[nums[i]]--;
            i++;
        }

        // Take the answer
        if(mp[nums[j]]>1) return true;

        j++;
    }
    return false;

}
```

### Problems
https://leetcode.com/problems/minimum-window-substring
https://leetcode.com/problems/minimum-size-subarray-sum
https://leetcode.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length
https://leetcode.com/problems/count-subarrays-with-fixed-bounds



## Concepts:
### Monotonic Increasing/Decreasing Ideas
- If we want the inc or dec element in the window. Instead of directly using priority queue to store elements we also store their index, as removing specific element from it is not that great. We check the top element and if that index falls within the window then it is answer else pop.
- Idea is, storing the elements in either inc or dec order od elements in the DS while looping the array.
- Using DS like Priority Queue, Stack, Queue, Deque to store the elements

```cadence
// https://leetcode.com/problems/sliding-window-maximum/description/

vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    int n=nums.size();

    priority_queue<pair<int,int>> heap; // Store element and index as well to check if it falls in window
   
    vector<int> ans;

    for(int i=0;i<n;i++){
        heap.push({nums[i],i});

        // Check if top element is in current window
        while(heap.top().second<=i-k){
            heap.pop();
        }
        
        if(i>=k-1)
        ans.push_back(heap.top().first);
    }

    return ans;    
}
```

Refer: [Youtube](https://www.youtube.com/watch?v=29OnjVQ-fk4&list=PLpIkg8OmuX-J2Ivo9YdY7bRDstPPTVGvN&index=12)

#### Problems:
https://leetcode.com/problems/sliding-window-maximum/description/
  
