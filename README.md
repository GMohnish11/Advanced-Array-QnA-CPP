# CPP-Advanced-Array-Questions

## Overview
This repository, `CPP-Advanced-Array-Questions`, contains a collection of intermediate-to-advanced array problems and their solutions in C++, developed by Mohnish Gupta. Designed for developers preparing for coding interviews or competitive programming, it includes challenging problems like finding the longest subarray with equal 0s and 1s, maximum product subarray, and spiral matrix traversal. It serves as a companion to the `CPP-Array-Questions` repository with higher complexity problems.

## Description
A collection of intermediate C++ array problems with solutions, including rotation, Kadane’s algorithm, and more. Ideal for coding practice and interviews, by Mohnish Gupta.

## Features
- **Advanced Problems**: Covers complex array techniques like prefix sums, two-pointer methods, and 2D matrix traversal.
- **C++ Solutions**: Efficient, well-commented code using modern C++ (e.g., `std::vector`, `unordered_map`).
- **Explanations**: Each problem includes a description, solution, time/space complexity, and edge case analysis in `cpp_advanced_array_questions.md`.
- **Testable Code**: Includes a `main.cpp` driver file to test solutions with custom inputs.
- **Modular Design**: Solutions are organized in `solutions/` for easy integration and testing.

## Installation
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/GMohnish11/CPP-Advanced-Array-Questions.git
   cd CPP-Advanced-Array-Questions
   ```
2. **Ensure C++ Compiler**:
   - Install a C++ compiler (e.g., `g++` via GCC) if not already present.
   - Verify: `g++ --version`.
3. **Compile and Run**:
   - Compile a specific solution:
     ```bash
     g++ solutions/solution1_longest_subarray.cpp -o longest_subarray
     ./longest_subarray
     ```
   - Or use `main.cpp` to test all solutions:
     ```bash
     g++ main.cpp -o test
     ./test
     ```

## Usage
### Exploring Problems
- Read `cpp_advanced_array_questions.md` for problem descriptions, solutions, and explanations.
- Problems include:
  1. Find the Longest Subarray with Equal 0s and 1s
  2. Maximum Product Subarray
  3. Trapping Rain Water
  4. Find the Median of Two Sorted Arrays
  5. Spiral Matrix Traversal

### Running Solutions
- Each solution is in the `solutions/` directory (e.g., `solution1_longest_subarray.cpp`).
- Modify `main.cpp` to test different inputs:
  ```cpp
  #include <vector>
  #include "solutions/solution1_longest_subarray.cpp"
  int main() {
      std::vector<int> arr = {0, 1, 0, 1, 1, 0};
      std::cout << findLongestSubarray(arr) << std::endl; // Output: 4
      return 0;
  }
  ```
- Compile and run as shown in the Installation section.

## Directory Structure
```
├── solutions/
│   ├── solution1_longest_subarray.cpp    # Longest subarray with equal 0s and 1s
│   ├── solution2_max_product.cpp         # Maximum product subarray
│   ├── solution3_trap_rain_water.cpp     # Trapping rain water
│   ├── solution4_median_arrays.cpp       # Median of two sorted arrays
│   ├── solution5_spiral_matrix.cpp       # Spiral matrix traversal
├── main.cpp                             # Driver code to test solutions
├── cpp_advanced_array_questions.md       # Problem descriptions and solutions
├── README.md                            # This file
```

## Contributing
Contributions are welcome! To contribute:
1. Fork the repository.
2. Create a branch: `git checkout -b feature/new-problem`.
3. Add your problem and solution in `solutions/` and update `cpp_advanced_array_questions.md`.
4. Commit changes: `git commit -m "Add new array problem"`.
5. Push: `git push origin feature/new-problem`.
6. Submit a Pull Request.

Report issues via the [Issues](https://github.com/GMohnish11/CPP-Advanced-Array-Questions/issues) tab.

## Acknowledgments
- **Author**: Mohnish Gupta
- **Institution**: St. Peter's Engineering College, Hyderabad
- **Inspiration**: Competitive programming platforms like LeetCode, Codeforces, and GeeksforGeeks
- **Resources**: C++ Standard Library and algorithm design references