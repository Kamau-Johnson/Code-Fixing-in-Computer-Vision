# Fixing My Code
<p float="center">
    <img src="Fix.png" width="50%" /> 
</p

```
Using try-except-else Blocks
```

Let's say we have a function that tries to find a value at a specific index in a list.
 

```python
def lookup(my_list, index):
    value = my_list[index]
    return f"The value at index {index} is {value}."


print(lookup(my_list=["a", "b", "c"], index=2))  # Index in range
print(lookup(my_list=["a", "b", "c"], index=5))  # Index out of range
```

    The value at index 2 is c.



    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    Cell In[1], line 7
          3     return f"The value at index {index} is {value}."
          6 print(lookup(my_list=["a", "b", "c"], index=2))  # Index in range
    ----> 7 print(lookup(my_list=["a", "b", "c"], index=5))  # Index out of range


    Cell In[1], line 2, in lookup(my_list, index)
          1 def lookup(my_list, index):
    ----> 2     value = my_list[index]
          3     return f"The value at index {index} is {value}."


    IndexError: list index out of range


This code raises an `IndexError` when an index is out of range. However, there may be situations where we want our program to handle this error gracefully and continue running, rather than stopping with an exception. 

One way to do this is by using `try-except-else` blocks. These blocks allow our program to attempt potentially error-prone operations and handle exceptions if they occur, thus enabling the code to continue executing. A `try` block attempts to execute potentially error-prone code. An `except` block specifies how to handle a particular type of exception if it occurs. An optional `else` block can be added to run code only if no exceptions were raised in the `try` block.

Below is an example demonstrating this approach, using similar logic to the previous example but implemented with `try-except-else` blocks:


```python
def lookup(my_list, index):
    try:
        value = my_list[index]
    except IndexError:
        return "Error: Index out of range."
    else:
        return f"The value at index {index} is {value}."


print(lookup(my_list=["a", "b", "c"], index=2))  # Index in range
print(lookup(my_list=["a", "b", "c"], index=5))  # Index out of range
```

    The value at index 2 is c.
    Error: Index out of range.


Now is your chance to improve code to be more fault-tolerant.

**Task 4.1.1:** Fix `divide_numbers` by adding `try-except-else` blocks.


```python
def divide_numbers(numerator, denominator):
    try:
        result = numerator / denominator

    except ZeroDivisionError:
        return "Error: Cannot divide by zero."

    else:
        return f"The result of {numerator} divided by {denominator} is {result}."


print(divide_numbers(numerator=10, denominator=2))  # Valid division
print(divide_numbers(numerator=10, denominator=0))  # Division by zero
```

    The result of 10 divided by 2 is 5.0.
    Error: Cannot divide by zero.


**Task 4.1.2:** Fix `find_user_name` by adding `try-except-else` blocks.


```python
users = {
    342: "Kwame Nkrumah",
    102: "Nguyen Thi Linh",
    423: "Muhammad bin Abdullah",
    654: "Fatou Diop",
    976: "Diana Martinez",
}


def find_user_name(user_id, users):
    try:
        user_name = users[user_id]

    except KeyError:
        return f"Error: User ID {user_id} not found."

    else:
        return f"User ID {user_id} corresponds to {user_name}."


print(find_user_name(user_id=654, users=users))
print(find_user_name(user_id=999, users=users))
```

    User ID 654 corresponds to Fatou Diop.
    Error: User ID 999 not found.


### Tuple Unpacking To Handle Variable Outputs

Below is a function that sometimes returns two values and other times returns three values. 


```python
import random
```


```python
def unpredictable_function():
    if random.choice([True, False]):
        return (1, 2)
    else:
        return (1, 2, 3)


for n in range(1, 11):
    print(f"Calling the function for the {n}th time")
    first, second = unpredictable_function()
    print(f"    First item: {first}")
    print(f"    Second item: {second}")
```

    Calling the function for the 1th time
        First item: 1
        Second item: 2
    Calling the function for the 2th time



    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    Cell In[15], line 10
          8 for n in range(1, 11):
          9     print(f"Calling the function for the {n}th time")
    ---> 10     first, second = unpredictable_function()
         11     print(f"    First item: {first}")
         12     print(f"    Second item: {second}")


    ValueError: too many values to unpack (expected 2)


This code raises a `ValueError`, which occurs when there are too many values to unpack.

We sometimes work with code that we cannot modify, such as when using a third-party library or calling an API. As software developers, it's our responsibility to write fault-tolerant code that can handle a variable number of outputs from that type of code.

Below is an example of using Python's tuple unpacking with `*` to manage a variable number of outputs. In tuple unpacking, you can prefix a variable name with an asterisk `*` to collect any remaining elements into a list. This is often called "star unpacking" or "extended unpacking". You can see that below with the variable `*rest`.


```python
for n in range(1, 11):
    print(f"Calling the function for the {n}th time")
    # Python tuple unpacking with * has been added on the left-hand side
    first, second, *rest = unpredictable_function()

    # Handle the common case (always present)
    print(f"    First item: {first}")
    print(f"    Second item: {second}")

    # Check if there's a third item
    if rest:
        print(f"    Third item: {rest[0]}")
    else:
        print("    No third item present")
```

    Calling the function for the 1th time
        First item: 1
        Second item: 2
        Third item: 3
    Calling the function for the 2th time
        First item: 1
        Second item: 2
        Third item: 3
    Calling the function for the 3th time
        First item: 1
        Second item: 2
        No third item present
    Calling the function for the 4th time
        First item: 1
        Second item: 2
        No third item present
    Calling the function for the 5th time
        First item: 1
        Second item: 2
        Third item: 3
    Calling the function for the 6th time
        First item: 1
        Second item: 2
        No third item present
    Calling the function for the 7th time
        First item: 1
        Second item: 2
        No third item present
    Calling the function for the 8th time
        First item: 1
        Second item: 2
        No third item present
    Calling the function for the 9th time
        First item: 1
        Second item: 2
        Third item: 3
    Calling the function for the 10th time
        First item: 1
        Second item: 2
        No third item present


Now it's your turn. Here is a `students` dictionary and a `get_student_info` function. The `get_student_info` function will return a list of just the values for a given entry. For `"Aisha"`, the function will return `[18, 'Pass']`. For `"Carlos"`, the function will return `[35]`. Use tuple unpacking to handle the output from a function that sometimes returns one item and other times returns two items. 


```python
students = {
    "Aisha": {"age": 18, "grade": "Pass"},
    "Carlos": {"age": 35},
    "Li Wei": {"age": 22, "grade": "Fail"},
    "Fatima": {"age": 27},
    "Yuki": {"age": 51, "grade": "Pass"},
}


def get_student_info(student_name, students):
    student_info = students[student_name]
    values = list(student_info.values())

    first, *rest = values

    print(f"    First item: {first}")

    if rest:
        print(f"    Remaining items: {rest}")
    else:
        print("    No additional items present")

    return values


# Example runs
print(get_student_info("Aisha", students))
print(get_student_info("Carlos", students))
```

        First item: 18
        Remaining items: ['Pass']
    [18, 'Pass']
        First item: 35
        No additional items present
    [35]


**Task 4.1.3:** Fix `print_student_info` by adding tuple unpacking `*`. Assume you can't modify `students` or `get_student_info`.


```python
def print_student_info(student_name, students):
    age, *rest = get_student_info(student_name, students)

    print(f"{student_name} is {age} years old.")

    # grade may or may not exist
    if rest:
        grade = rest[0]
        print(f"{student_name} earned a {grade}.")


print_student_info(student_name="Aisha", students=students)
print_student_info(student_name="Carlos", students=students)
```

        First item: 18
        Remaining items: ['Pass']
    Aisha is 18 years old.
    Aisha earned a Pass.
        First item: 35
        No additional items present
    Carlos is 35 years old.


To recap, we've explored how to write fault-tolerant Python code using `try-except-else` blocks and tuple unpacking. `try-except-else` blocks allow us to gracefully handle errors ensuring our programs don't crash unexpectedly. Tuple unpacking with `*` helps manage functions with variable outputs, enabling our code to seamlessly adapt to different scenarios.

---
&#169; 2024 by [WorldQuant University](https://www.wqu.edu/)
