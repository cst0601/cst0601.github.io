---
title: C/C++ Code Snippets
author: chikuma
date: 2023-09-21 15:00:00 -0700
categories: [Leetcode]
tags: [Programming]
render_with_liquid: false
---

This post is about some C++ code snippets that might be useful when doing online
assessment (and this post might continue to grow). Sometimes we just couldn't
remember how to do a certain operation and can't access StackOverflow for quick
answers. I definitely learned this the hard way.

Or we possibility should do our online assessment in Python to avoid these sort
of problems.

## Splitting a string using string delimiter
```cpp
std::string str = "The sentence to be split";
std::string delimiter = " ";
std::vector<std::string> result;

size_t pos = 0;
std::string token;
while((pos = str.find(delimiter)) != std::string::npos) {
    token = str.substr(0, pos);
    result.push_back(token);
    str.erase(0, pos + delimiter.length());
}
result.push_back(str);
```

### Another method using `stringstream`:
```cpp
std::string str = "The sentence to be split";
std::stringstream ss(str);
std::vector<std::string> result;
std::string token;

while (ss >> token) {
    result.push_back(token);
}
```

## CUDA Error Handling Macro

Not actually C++ code, but could be fitted else where.
Saw this trick from CUDA-By-Example.

```cpp
static void HandleError(cudaError_t err, const char *file, int line) {
    if (err != cudaSuccess) {
        printf("%s in %s at line %d/n", cudaGetErrorString(err), file, line);
        exit(EXIT_FAILURE);
    }
}

#define HANDLE_ERROR( err ) (HandleError (err, __FILE__, __LINE__))
```
Then use the macro `HANDLE_ERROR` as follow:
```cpp
HANDLE_ERROR( cudaMemcpy(dev_a, a, N * sizeof(int), cudaMemcpyHostToDevice) );
```