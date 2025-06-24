# Advanced Array Questions and Solutions in C++

This repository contains a collection of intermediate-to-advanced array problems and their solutions in C++, designed for developers preparing for coding interviews or competitive programming. Each problem includes a description, a C++ solution, and a detailed explanation. Authored by Mohnish Gupta, this is a companion to the `CPP-Array-Questions` repository with more challenging problems.

## Table of Contents
1. [Find the Longest Subarray with Equal 0s and 1s](#find-the-longest-subarray-with-equal-0s-and-1s)
2. [Maximum Product Subarray](#maximum-product-subarray)
3. [Trapping Rain Water](#trapping-rain-water)
4. [Find the Median of Two Sorted Arrays](#find-the-median-of-two-sorted-arrays)
5. [Spiral Matrix Traversal](#spiral-matrix-traversal)

---

## Find the Longest Subarray with Equal 0s and 1s

### Problem
Given a binary array, find the length of the longest subarray with an equal number of 0s and 1s. For example, if `arr = [0, 1, 0, 1, 1, 0]`, the longest subarray is `[0, 1, 0, 1]` with length 4.

### Solution
```cpp
#include <vector>
#include <unordered_map>
int findLongestSubarray(std::vector<int>& arr) {
    std::unordered_map<int, int> sum_index;
    int sum = 0, max_length = 0;
    sum_index[0] = -1; // Initialize for subarray starting at index 0
    
    for (int i = 0; i < arr.size(); i++) {
        sum += (arr[i] == 0 ? -1 : 1); // Treat 0 as -1, 1 as +1
        if (sum_index.find(sum) != sum_index.end()) {
            max_length = std::max(max_length, i - sum_index[sum]);
        } else {
            sum_index[sum] = i;
        }
    }
    return max_length;
}
```

### Explanation
- **Approach**: Convert 0s to -1 and 1s to +1, then use a prefix sum technique. Track the cumulative sum and store the first occurrence of each sum in a hash map. If a sum repeats, a subarray with equal 0s and 1s exists between those indices.
- **Time Complexity**: O(n), single pass with hash map operations.
- **Space Complexity**: O(n), for the hash map.
- **Edge Cases**: Handles empty arrays, arrays with no valid subarray, or all 0s/1s.

---

## Maximum Product Subarray

### Problem
Given an array of integers, find the maximum product of any contiguous subarray. For example, if `arr = [2, 3, -2, 4]`, the maximum product is `6` (subarray `[2, 3]`).

### Solution
```cpp
#include <vector>
int maxProductSubarray(std::vector<int>& arr) {
    int max_so_far = arr[0], max_ending_here = arr[0], min_ending_here = arr[0];
    for (int i = 1; i < arr.size(); i++) {
        int temp = max_ending_here;
        max_ending_here = std::max({arr[i], max_ending_here * arr[i], min_ending_here * arr[i]});
        min_ending_here = std::min({arr[i], temp * arr[i], min_ending_here * arr[i]});
        max_so_far = std::max(max_so_far, max_ending_here);
    }
    return max_so_far;
}
```

### Explanation
- **Approach**: Similar to Kadane’s algorithm but tracks both maximum and minimum products at each step due to negative numbers. Update the global maximum product (`max_so_far`) with each iteration.
- **Time Complexity**: O(n), single pass through the array.
- **Space Complexity**: O(1), uses constant extra space.
- **Edge Cases**: Handles negative numbers, zeros, and single-element arrays.

---

## Trapping Rain Water

### Problem
Given an array representing elevation heights, calculate how much water can be trapped between bars after raining. For example, if `arr = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]`, the trapped water is `6` units.

### Solution
```cpp
#include <vector>
int trapRainWater(std::vector<int>& height) {
    int n = height.size(), water = 0;
    int left = 0, right = n - 1, left_max = 0, right_max = 0;
    
    while (left < right) {
        if (height[left] <= height[right]) {
            if (height[left] >= left_max) {
                left_max = height[left];
            } else {
                water += left_max - height[left];
            }
            left++;
        } else {
            if (height[right] >= right_max) {
                right_max = height[right];
            } else {
                water += right_max - height[right];
            }
            right--;
        }
    }
    return water;
}
```

### Explanation
- **Approach**: Use a two-pointer technique. Maintain `left_max` and `right_max` to track the maximum heights from both ends. Water at each position is the minimum of `left_max` and `right_max` minus the current height.
- **Time Complexity**: O(n), single pass with two pointers.
- **Space Complexity**: O(1), constant space.
- **Edge Cases**: Handles arrays with no trapped water, single bars, or all same heights.

---

## Find the Median of Two Sorted Arrays

### Problem
Given two sorted arrays `nums1` and `nums2` of sizes `m` and `n`, find the median of the merged sorted array. For example, if `nums1 = [1, 3]` and `nums2 = [2]`, the median is `2.0`.

### Solution
```cpp
#include <vector>
double findMedianSortedArrays(std::vector<int>& nums1, std::vector<int>& nums2) {
    if (nums1.size() > nums2.size()) return findMedianSortedArrays(nums2, nums1);
    
    int m = nums1.size(), n = nums2.size();
    int left = 0, right = m;
    
    while (left <= right) {
        int partitionX = (left + right) / 2;
        int partitionY = (m + n + 1) / 2 - partitionX;
        
        int maxLeftX = (partitionX == 0) ? INT_MIN : nums1[partitionX - 1];
        int minRightX = (partitionX == m) ? INT_MAX : nums1[partitionX];
        int maxLeftY = (partitionY == 0) ? INT_MIN : nums2[partitionY - 1];
        int minRightY = (partitionY == n) ? INT_MAX : nums2[partitionY];
        
        if (maxLeftX <= minRightY && maxLeftY <= minRightX) {
            if ((m + n) % 2 == 0) {
                return (std::max(maxLeftX, maxLeftY) + std::min(minRightX, minRightY)) / 2.0;
            } else {
                return std::max(maxLeftX, maxLeftY);
            }
        } else if (maxLeftX > minRightY) {
            right = partitionX - 1;
        } else {
            left = partitionX + 1;
        }
    }
    return 0.0; // Should not reach here
}
```

### Explanation
- **Approach**: Use binary search on the smaller array to find the correct partition such that the left and right halves of the merged array are balanced. Compute the median based on whether the total length is odd or even.
- **Time Complexity**: O(log(min(m, n))), binary search on the smaller array.
- **Space Complexity**: O(1), constant space.
- **Edge Cases**: Handles empty arrays, odd/even total lengths, and arrays of different sizes.

---

## Spiral Matrix Traversal

### Problem
Given an `m x n` matrix, return all elements in spiral order (clockwise from top-left). For example, if `matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]`, the result is `[1, 2, 3, 6, 9, 8, 7, 4, 5]`.

### Solution
```cpp
#include <vector>
std::vector<int> spiralOrder(std::vector<std::vector<int>>& matrix) {
    std::vector<int> result;
    if (matrix.empty()) return result;
    
    int m = matrix.size(), n = matrix[0].size();
    int top = 0, bottom = m - 1, left = 0, right = n - 1;
    
    while (top <= bottom && left <= right) {
        // Traverse right
        for (int j = left; j <= right; j++) result.push_back(matrix[top][j]);
        top++;
        // Traverse down
        for (int i = top; i <= bottom; i++) result.push_back(matrix[i][right]);
        right--;
        if (top <= bottom) {
            // Traverse left
            for (int j = right; j >= left; j--) result.push_back(matrix[bottom][j]);
            bottom--;
        }
        if (left <= right) {
            // Traverse up
            for (int i = bottom; i >= top; i--) result.push_back(matrix[i][left]);
            left++;
        }
    }
    return result;
}
```

### Explanation
- **Approach**: Use four pointers (`top`, `bottom`, `left`, `right`) to traverse the matrix in a spiral order, layer by layer, shrinking the boundaries after each direction.
- **Time Complexity**: O(m * n), visits each element once.
- **Space Complexity**: O(1), excluding output array.
- **Edge Cases**: Handles single-row/column matrices, empty matrices, and non-square matrices.

---

## How to Run
1. Clone the repository:
   ```bash
   git clone https://github.com/GMohnish11/CPP-Advanced-Array-Questions.git
   cd CPP-Advanced-Array-Questions
   ```
2. Compile and run a solution:
   ```bash
   g++ solutions/solution1_longest_subarray.cpp -o longest_subarray
   ./longest_subarray
   ```
3. Use `main.cpp` to test solutions with custom inputs:
   ```cpp
   #include <vector>
   #include "solutions/solution1_longest_subarray.cpp"
   int main() {
       std::vector<int> arr = {0, 1, 0, 1, 1, 0};
       std::cout << findLongestSubarray(arr) << std::endl; // Output: 4
       return 0;
   }
   ```

## Directory Structure
```
├── solutions/
│   ├── solution1_longest_subarray.cpp    # Longest subarray with equal 0s and 1s
│   ├── solution2_max_product.cpp         # Maximum product subarray
│   ├── solution3_trap_rain_water.cpp     # Trapping rain water
│   ├── solution4_median_arrays.cpp       # Median of two sorted arrays
│   ├── solution5_spiral_matrix.cpp       # Spiral matrix traversal
├── main.cpp                             # Driver code to test solutions
├── cpp_advanced_array_questions.md       # This file
├── README.md                            # Repository overview (separate file)
└── LICENSE                              # MIT License
```

## Contributing
Contributions are welcome! To contribute:
1. Fork the repository.
2. Create a branch: `git checkout -b feature/new-problem`.
3. Add your problem and solution in `solutions/`.
4. Update this Markdown file with the new problem.
5. Submit a Pull Request.

Report issues via the [Issues](https://github.com/GMohnish11/CPP-Advanced-Array-Questions/issues) tab.

## License
Licensed under the MIT License. See [LICENSE](LICENSE) for details.

## Acknowledgments
- **Author**: Mohnish Gupta
- **Institution**: St. Peter's Engineering College, Hyderabad
- **Inspiration**: Competitive programming platforms like LeetCode, Codeforces, and GeeksforGeeks
- **Resources**: Algorithm design references and C++ Standard Library

## Contact
For inquiries, contact Mohnish Gupta via GitHub issues.