# Applying Functions to NumPy Arrays: A Primer

## Arithmetic Operations with NumPy Arrays

Two arrays of the same shape can undergo basic arithmetic operations. The operations are performed element-wise, meaning they're applied to each pair of corresponding elements. Suppose we have two grade arrays of students from two subjects. By adding these arrays, we can calculate the total grades:

```Python

subject1_grades = np.array([88, 90, 75, 92, 85])
subject2_grades = np.array([92, 85, 78, 90, 88])

total_grades = subject1_grades + subject2_grades

print("Total grades:", total_grades)  # Output: Total grades: [180 175 153 182 173]
```
The two arrays are added element-wise in this code to calculate the total grades.

## Introduction to Universal Functions (ufuncs)

NumPy's Universal Functions (also called ufuncs) perform element-wise operations on arrays, including mathematical functions like sin, cos, log, and sqrt. Let's look at a use case:

```Python

angles_degrees = np.array([0, 30, 45, 60, 90])
angles_radians = np.radians(angles_degrees)
sin_values = np.sin(angles_radians)

print("Sine of angles:", sin_values)  # Output: Sine of angles: [0. 0.5 0.70710678 0.8660254 1.]
```
This code applies np.sin universal function to each array element. As np.sin expects its input in radians, we first transform degrees to radians with np.radians, applying it to each array element similarly.

## Extending NumPy with Custom Functions

NumPy allows the application of a custom function to each element of the array separately by transforming the target function with np.vectorize. Let's create a function to check the parity of a number:

```Python

def is_even(n):
    return n % 2 == 0

vectorized_is_even = np.vectorize(is_even)

numbers = np.array([1, 2, 3, 4, 5])
results = vectorized_is_even(numbers)

print("Results:", results).  # Output: Results: [False True False True False]
```
The vectorized_is_even function returns an array indicating whether each value in numbers is even.

