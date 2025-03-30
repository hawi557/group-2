```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <chrono>

void simple_sort(std::vector<int>& arr) {
    for (size_t i = 0; i < arr.size() - 1; ++i) {
        for (size_t j = i + 1; j < arr.size(); ++j) {
            if (arr[i] > arr[j]) {
                std::swap(arr[i], arr[j]);
            }
        }
    }
}

void bubble_sort(std::vector<int>& arr) {
    size_t n = arr.size();
    int swaps = 0;
    for (size_t i = 0; i < n - 1; i++) {
        for (size_t j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                std::swap(arr[j], arr[j + 1]);
                swaps++;
            }
        }
    }
}

void insertion_sort(std::vector<int>& arr) {
    size_t n = arr.size();
    int comparisons = 0;
    for (size_t i = 1; i < n; ++i) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
            comparisons++;
        }
        arr[j + 1] = key;
    }
}

void selection_sort(std::vector<int>& arr) {
    size_t n = arr.size();
    int comparisons = 0;
    for (size_t i = 0; i < n - 1; i++) {
        int min_index = i;
        for (size_t j = i + 1; j < n; j++) {
            comparisons++;
            if (arr[j] < arr[min_index]) {
                min_index = j;
            }
        }
        std::swap(arr[i], arr[min_index]);
    }
}

void print_array(const std::vector<int>& arr) {
    for (int i : arr) {
        std::cout << i << " ";
    }
    std::cout << std::endl;
}

void measure_performance(const std::string& algorithm_name, std::vector<int>& arr) {
    std::chrono::steady_clock::time_point start = std::chrono::steady_clock::now();
    std::chrono::steady_clock::time_point end;
    int comparisons = 0;
    int swaps = 0;

    if (algorithm_name == "simple_sort") {
        simple_sort(arr);
    } else if (algorithm_name == "bubble_sort") {
        bubble_sort(arr);
    } else if (algorithm_name == "insertion_sort") {
        insertion_sort(arr);
    } else if (algorithm_name == "selection_sort") {
        selection_sort(arr);
    } else {
        std::cerr << "Invalid sorting algorithm" << std::endl;
        return;
    }

    end = std::chrono::steady_clock::now();
    auto duration = std::chrono::duration_cast<std::chrono::microseconds>(end - start).count();

    if (algorithm_name == "bubble_sort") {
        std::cout << "Number of swaps in " << algorithm_name << ": " << swaps << std::endl;
    } else if (algorithm_name == "insertion_sort" || algorithm_name == "selection_sort") {
        std::cout << "Number of comparisons in " << algorithm_name << ": " << comparisons << std::endl;
    }
    std::cout << "Time taken by " << algorithm_name << " is " << duration << " microseconds" << std::endl;
}
return 0;
}
