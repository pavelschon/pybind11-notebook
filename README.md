# Running pybin11 under Jupyter Notebook with Xeus-Cling

## Initial setup
```bash
conda install -c conda-forge xeus-cling
conda install -c conda-forge pybind11
conda install -c conda-forge notebook
```

## Notebook

```c++
#pragma cling add_include_path("/home/jupyter/miniconda3/include/python3.9/")
#pragma cling add_library_path("/home/jupyter/miniconda3/lib")
#pragma cling load("python3.9")

#include <pybind11/embed.h>
#include <iostream>

namespace py = pybind11;

void py_print( py::object o )
{
    std::cout << py::str(o).cast<std::string>() << "\n";
};

py::scoped_interpreter python;
```
---

```c++
py::str s{"Hello world"};
```
---
```c++
py_print(s);
```
```
Hello world
```
