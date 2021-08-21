# Jupyter Notebook running pybind11 program with Xeus-Cling

![pybind11](pybind11.png)

## Initial setup
```bash
conda install -c conda-forge xeus-cling
conda install -c conda-forge pybind11
conda install -c conda-forge notebook
```

## The code

```c++
#pragma cling add_include_path("/home/jupyter/miniconda3/include/python3.9/")
#pragma cling add_library_path("/home/jupyter/miniconda3/lib")
#pragma cling load("python3.9")

#include <pybind11/embed.h>
#include <iostream>

namespace py = pybind11;

void py_print(py::object o)
{
    std::cout << py::str(o).cast<std::string>() << "\n";
};

py::scoped_interpreter python;

py::str s{"Hello world"};
py_print(s);
```
## Remarks
* The buildin function `py::print()` prints into the terminal where you're running jupyter notebook, hence using custom `py_print()`.
* Exception handling with `catch(const py::error_already_set& e)` sometimes works, sometimes not. Suggestions how to improve it are welcomed.
