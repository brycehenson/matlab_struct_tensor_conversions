# Matlab Structure (nd)Array Conversions
**[Bryce M. Henson](https://github.com/brycehenson)**  
convert between the various ways n-dimensional arrays (sometimes called tensors) can be stored in (or interact with) structures  
**Status:** This Code is **ready** for use in other projects. Unit Testing is implemented. Round-Robin testing is implemented and **passing**.
[![View matlab_struct_array_conversions on File Exchange](https://www.mathworks.com/matlabcentral/images/matlab-file-exchange.svg)](https://www.mathworks.com/matlabcentral/fileexchange/77440-matlab_struct_array_conversions)

| ![diagram of the conversion between struct-tensor types](/figs/diagram.png "Fig1") | 
|:--:| 
 **Figure 1**- Schematic of the different storage types and how the conversion maps elements.|

## Motivation
matlab has 3 distinct way you can store n-dimensional arrays (aka tensors, multidimensional arrays, or nd-array) in structures.
- ***(A)*** structure with an nd-array in each field (aka. struct of tensors) (fig.1 right)
  - I think this is the easiest to work with
  - it does not enforce dimension matching things can go wrong if you not careful about building/ modifying each field
  - access and creation is the simplest
- ***(B)*** Cell nd-array of structures (fig.1 top left)
  - this is the most flexible as the cell in each nd-array can have completely different fields
  - it is very difficult to query as you must handle the possibly different fields present
- ***(C)*** structure nd-array(tensor) (fig.1 bottom left)
  - this can be hard to build as you cant set multiple values at the same time.
  - the result of queries do not preserve dimensionality eg ```test_struct_array(1,1:2,1:3).data1```
  - this format is very confusing to work with and leads to some pretty slow approaches (both in dev time and computer time).
  - **For your own sanity i discourage this format**

  
Each has their own advantages, frustration and quirks. Conventions (including in matlab) vary and we would like a way to convert between these formats.

## Code
This package provides conversions ***(A)*** <-> ***(B)*** and ***(A)*** <-> ***(C)***
- (***(B)*** -> ***(A)***) cell_array_of_struct_to_struct_of_array
- (***(A)*** -> ***(B)***) struct_of_array_to_cell_array_of_struct

- (***(C)*** -> ***(A)***) struct_array_to_struct_of_array
- (***(A)*** -> ***(C)***)  struct_of_array_to_struct_array

It also provides match_tensor_sizes sizes which is used in struct_of_tensor_to_cell_tensor_of_struct to repeat a smaller tensor along its singleton dimensions to match a larger tensor.

All 6 conversions can handle arbitrary dimensionality arrays and structures of any depth.


## TODO
- [ ] full test script including error cases
  - [x] roundrobin tests
- [ ] option in struct_of_tensor_to_cell_tensor_of_struct to use nan instead of repeating along singleton dim.
- [ ] better speed bencmarking
- [ ] standard funciton headers including examples
- [x] pretty picture to represent conversions
- [ ] add to fileExchange






