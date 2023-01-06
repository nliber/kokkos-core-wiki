
# `transform`

Header File: `Kokkos_StdAlgorithms.hpp`

```c++
namespace Kokkos{
namespace Experimental{

template <class ExecutionSpace, class InputIterator, class OutputIterator, class UnaryOperation>
OutputIterator transform(const ExecutionSpace& exespace,                        (1)
                         InputIterator first_from, InputIterator last_from,
                         OutputIterator first_to,
                         UnaryOperation unary_op);

template <class ExecutionSpace, class InputIterator, class OutputIterator, class UnaryOperation>
OutputIterator transform(const std::string& label,                              (2)
                         const ExecutionSpace& exespace,
                         InputIterator first_from, InputIterator last_from,
                         OutputIterator d_first,
                         UnaryOperation unary_op);

template <
  class ExecutionSpace,
  class DataType1, class... Properties1,
  class DataType2, class... Properties2,
  class UnaryOperation
>
auto transform(const ExecutionSpace& exespace,                                  (3)
               const Kokkos::View<DataType1, Properties1...>& source,
               Kokkos::View<DataType2, Properties2...>& dest,
               UnaryOperation unary_op);

template <
  class ExecutionSpace,
  class DataType1, class... Properties1,
  class DataType2, class... Properties2,
  class UnaryOperation
>
auto transform(const std::string& label, const ExecutionSpace& exespace,        (4)
               const Kokkos::View<DataType1, Properties1...>& source,
               Kokkos::View<DataType2, Properties2...>& dest,
               UnaryOperation unary_op);

template <
  class ExecutionSpace,
  class InputIterator1, class InputIterator2, class OutputIterator,
  class BinaryOperation
>
OutputIterator transform(const ExecutionSpace& exespace,                        (5)
                         InputIterator1 first_from1, InputIterator1 last_from1,
                         InputIterator2 first_from2, OutputIterator first_to,
                         BinaryOperation binary_op);

template <
  class ExecutionSpace,
  class InputIterator1, class InputIterator2, class OutputIterator,
  class BinaryOperation
>
OutputIterator transform(const std::string& label,                              (6)
                         const ExecutionSpace& exespace,
                         InputIterator1 first_from1, InputIterator1 last_from1,
                         InputIterator2 first_from2, OutputIterator first_to,
                         BinaryOperation binary_op);

template <
  class ExecutionSpace,
  class DataType1, class... Properties1,
  class DataType2, class... Properties2,
  class DataType3, class... Properties3,
  class BinaryOperation
>
auto transform(const ExecutionSpace& exespace,                                  (7)
               const Kokkos::View<DataType1, Properties1...>& source1,
               const Kokkos::View<DataType2, Properties2...>& source2,
               Kokkos::View<DataType3, Properties3...>& dest,
               BinaryOperation binary_op);

template <
  class ExecutionSpace,
  class DataType1, class... Properties1,
  class DataType2, class... Properties2,
  class DataType3, class... Properties3,
  class BinaryOperation
>
auto transform(const std::string& label, const ExecutionSpace& exespace,        (8)
               const Kokkos::View<DataType1, Properties1...>& source1,
               const Kokkos::View<DataType2, Properties2...>& source2,
               Kokkos::View<DataType3, Properties3...>& dest,
               BinaryOperation binary_op);

} //end namespace Experimental
} //end namespace Kokkos
```

## Description

- Overloads (1,2): applies the given *unary* operation to all elements in the
range `[first_from, last_from)` stores the result in the range starting at `first_to`

- Overloads (3,4): applies the given *unary* operation to all elements in
the `source` view and stores the result in the `dest` view.

- Overloads (5,6): applies the given *binary* operation to pair of elements
from the ranges `[first_from1, last_from1)` and `[first_from2, last_from2]`
and stores the result in range starting at `first_to`

- Overloads (7,8): applies the given *binary* operation to pair of elements
from the views `source1, source2` and stores the result in `dest` view


## Parameters and Requirements

- `exespace`:
  - execution space instance
- `label`:
  - used to name the implementation kernels for debugging purposes
  - for 1,3,5,7, the default string is: "Kokkos::transform_iterator_api_default"
  - for 2,4,6,8, the default string is: "Kokkos::transform_view_api_default"
- `first_from, last_from, first_from1, first_from2`:
  - ranges of elements to tranform
  - must be *random access iterators*
  - must be valid ranges, i.e., `first_from >= last_from`, `first_from1 >= last_from2`
  - must be accessible from `exespace`
- `first_to`:
  - beginning of the range to write to
  - must be a *random access iterator*
  - must be accessible from `exespace`
- `source, source1, source2`:
  - source views to transform
  - must be accessible from `exespace`
- `dest`:
  - destination view to write to
  - must be accessible from `exespace`


## Return

Iterator to the element *after* the last element transformed.
